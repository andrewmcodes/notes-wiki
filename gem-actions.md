# Gem Actions

1. Simple

```yaml
name: Ruby

on: [push,pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Ruby
      uses: ruby/setup-ruby@v1
      with:
        ruby-version: 3.0.0
    - name: Run the default task
      run: |
        gem install bundler -v 2.2.7
        bundle install
        bundle exec rake
```

2. Release Please Action

```yaml
name: release

on:
  push:
    branches:
      - main
jobs:
  release-please:
    runs-on: ubuntu-latest
    steps:
      - uses: GoogleCloudPlatform/release-please-action@v2
        id: release
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          release-type: ruby
          package-name: CHANGEME
          bump-minor-pre-major: true
          version-file: "lib/CHANGEME/version.rb"
      - uses: actions/checkout@v2
        if: ${{ steps.release.outputs.release_created }}
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: 3.0.0
        if: ${{ steps.release.outputs.release_created }}
      - run: |
          gem install bundler -v 2.2.7
          bundle install
          bundle exec rake
        if: ${{ steps.release.outputs.release_created }}
      - name: release gem
        run: |
          mkdir -p $HOME/.gem
          touch $HOME/.gem/credentials
          chmod 0600 $HOME/.gem/credentials
          printf -- "---\n:rubygems_api_key: ${GEM_HOST_API_KEY}\n" > $HOME/.gem/credentials
          gem build *.gemspec
          gem push *.gem
        env:
          GEM_HOST_API_KEY: "${{secrets.RUBYGEMS_AUTH_TOKEN}}"
        if: ${{ steps.release.outputs.release_created }}
```
