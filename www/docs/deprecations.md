# Deprecation notices

This page is used to list deprecation notices across GoReleaser.

Deprecated options will be removed after ~6 months from the time they were
deprecated.

You can check your use of deprecated configurations by running:

```sh
goreleaser check
```

## Active deprecation notices

<!--

Template for new deprecations:

### property

> since yyyy-mm-dd

Description.

=== "Before"

    ``` yaml
    foo: bar
    ```

=== "After"
    ``` yaml
    foo: bar
    ```

-->

### variables

> since 2022-01-20 (v1.4.0)

On [GoReleaser PRO][pro], custom variables should now be prefixed with `.Var`.

=== "Before"

    ``` yaml
    variables:
      foo: bar
    some_template: 'lala-{{ .foo }}'
    ```

=== "After"

    ``` yaml
    variables:
      foo: bar
    some_template: 'lala-{{ .Var.foo }}'
    ```

### nfpm.empty_folders

> since 2021-11-14  (v1.0.0)

nFPM empty folders is now deprecated in favor of a `dir` content type:

=== "Before"

    ``` yaml
    nfpms:
    - empty_folders:
      - /foo/bar
    ```

=== "After"
    ``` yaml
    nfpms:
    - contents:
      - dst: /foo/bar
        type: dir
    ```

### godownloader

> since 2021-10-13 (all)

GoDownloader, the install script generator, wasn't been updated for a long time and is now officially deprecated.
The website and all install scripts will be taken out in 6 months.
You can still use any of the other install methods.

### builds for windows/arm64

> since 2021-08-16 (v0.175.0)

Since Go 1.17, `windows/arm64` is a valid target.

Prior to v0.175.0, GoReleaser would just ignore this target.
Since in Go 1.17 it is now a valid target, GoReleaser will build it if the Go version being used is 1.17 or later.

If you want to make sure it is ignored in the future, you need to add this to your build config:

```yaml
ignore:
- goos: windows
  goarch: arm64
```

If you try to use new versions of GoReleaser with Go 1.16 or older, it will warn about it until this deprecation warning expires, after that your build will likely fail.

### docker.use_buildx

> since 2021-06-26 (v0.172.0)

`use_buildx` is deprecated in favor of the more generalist `use`, since now it also allow other options in the future:

Change this:

=== "Before"
    ```yaml
    dockers:
      -
        use_buildx: true
    ```

=== "After"
    ```yaml
    dockers:
      -
        use: buildx
    ```

### builds for darwin/arm64

> since 2021-02-17 (v0.157.0)

Since Go 1.16, `darwin/arm64` is macOS on Apple Silicon instead of `iOS`.

Prior to v0.156.0, GoReleaser would just ignore this target.
Since in Go 1.16 and later it is a valid target, GoReleaser will now build it if the Go version being used is 1.16 or later.

If you want to make sure it is ignored in the future, you need to add this to your build config:

```yaml
ignore:
- goos: darwin
  goarch: arm64
```

If you try to use new versions of GoReleaser with Go 1.15 or older, it will warn about it until this deprecation warning expires, after that your build will likely fail.

## Expired deprecation notices

The following options were deprecated in the past and were already removed.

### Skipping SemVer Validations

> since 2021-02-28 (v0.158.0), removed 2021-09-22 (v0.180.0)

GoReleaser skips SemVer validations when run with `--skip-validation` or `--snapshot`.
This causes other problems later, such as [invalid Linux packages](https://github.com/goreleaser/goreleaser/issues/2081).
Because of that, once this deprecation expires, GoReleaser will hard fail on non-semver versions, as stated on our [limitations page](https://goreleaser.com/limitations/semver/).

### docker.builds

> since 2021-01-07 (v0.154.0), removed 2021-08-13 (v0.175.0)

`builds` is deprecated in favor of `ids`, since now it also allows to copy nfpm packages:

Change this:

=== "Before"
    ```yaml
    dockers:
      -
        builds: ['a', 'b']
    ```

=== "After"
    ```yaml
    dockers:
      -
        ids: ['a', 'b']
    ```

### docker.binaries

> since 2021-01-07 (v0.154.0), removed 2021-08-13 (v0.175.0)

`binaries` is deprecated and now does nothing.
If you want to filter something out, use the `ids` property.

Change this:

=== "Before"
    ```yaml
    dockers:
      -
        binaries: ['foo']
    ```

=== "After"
    ```yaml
    dockers:
      -
        ids: ['foo']
    ```

### nfpms.files

> since 2020-12-21 (v0.149.0), removed 2021-07-26 (v0.172.0)

`files` is deprecated in favor of `contents` (check [this page](https://goreleaser.com/customization/nfpm/) for more details):

Change this:

=== "Before"
    ```yaml
    nfpms:
      -
        files:
          foo: bar
    ```

=== "After"
    ```yaml
    nfpms:
      -
        contents:
          - src: foo
            dst: bar
    ```

### nfpms.config_files

> since 2020-12-21 (v0.149.0), removed 2021-07-26 (v0.172.0)

`config_files` is deprecated in favor of `contents` (check [this page](https://goreleaser.com/customization/nfpm/) for more details):

Change this:

=== "Before"
    ```yaml
    nfpms:
      -
        config_files:
          foo: bar
    ```

=== "After"
    ```yaml
    nfpms:
      -
        contents:
          - src: foo
            dst: bar
            type: config
    ```

### nfpms.symlinks

> since 2020-12-21 (v0.149.0), removed 2021-07-26 (v0.172.0)

`symlinks` is deprecated in favor of `contents` (check [this page](https://goreleaser.com/customization/nfpm/) for more details):

Change this:

=== "Before"
    ```yaml
    nfpms:
      -
        symlinks:
          foo: bar
    ```

=== "After"
    ```yaml
    nfpms:
      -
        contents:
          - src: foo
            dst: bar
            type: symlink
    ```

### nfpms.rpm.ghost_files

> since 2020-12-21 (v0.149.0), removed 2021-07-26 (v0.172.0)

`rpm.ghost_files` is deprecated in favor of `contents` (check [this page](https://goreleaser.com/customization/nfpm/) for more details):

Change this:

=== "Before"
    ```yaml
    nfpms:
      -
        rpm:
          ghost_files:
            - foo
    ```

=== "After"
    ```yaml
    nfpms:
      -
        contents:
          - dst: bar
            type: ghost
            packager: rpm # optional
    ```

### nfpms.rpm.config_noreplace_files

> since 2020-12-21 (v0.149.0), removed 2021-07-26 (v0.172.0)

`rpm.config_noreplace_files` is deprecated in favor of `contents` (check [this page](https://goreleaser.com/customization/nfpm/) for more details):

Change this:

=== "Before"
    ```yaml
    nfpms:
      -
        rpm:
          config_noreplace_files:
            foo: bar
    ```

=== "After"
    ```yaml
    nfpms:
      -
        contents:
          - src: foo
            dst: bar
            type: config|noreplace
            packager: rpm # optional
    ```


### nfpms.deb.version_metadata

> since 2020-12-21 (v0.149.0), removed 2021-07-26 (v0.172.0)

`deb.version_metadata` is deprecated in favor of `version_metadata` (check [this page](https://goreleaser.com/customization/nfpm/) for more details):

Change this:

=== "Before"
    ```yaml
    nfpms:
      -
        deb:
          version_metadata: beta1
    ```

=== "After"
    ```yaml
    nfpms:
      -
        version_metadata: beta1
    ```

### brews.github

> since 2020-07-06 (v0.139.0), removed 2021-01-04 (v0.152.0)

GitHub section was deprecated in favour of `tap` which
reflects Homebrew's naming convention. GitHub will be picked
automatically when GitHub token is passed.

Change this:

=== "Before"
    ```yaml
    brews:
      -
        github:
          owner: goreleaser
          name: homebrew-tap
    ```

=== "After"
    ```yaml
    brews:
      -
        tap:
          owner: goreleaser
          name: homebrew-tap
    ```

### brews.gitlab

> since 2020-07-06 (v0.139.0), removed 2021-01-04 (v0.152.0)

GitLab section was deprecated in favour of `tap` which
reflects Homebrew's naming convention. GitLab will be picked
automatically when GitLab token is passed.

Change this:

=== "Before"
    ```yaml
    brews:
      -
        gitlab:
          owner: goreleaser
          name: homebrew-tap
    ```

=== "After"
    ```yaml
    brews:
      -
        tap:
          owner: goreleaser
          name: homebrew-tap
    ```

### puts

> since 2019-11-15, removed 2020-04-14 (v0.132.0)

The HTTP upload support was extended to also accept `POST` as a method,
so the name `puts` kind of lost its meaning.

=== "Before"

    ``` yaml
    puts:
    - ...
    ```

=== "After"
    ``` yaml
    uploads:
    - ...
    ```

Also note that secrets environment variable name prefixes have changed from
`PUT_` to `UPLOAD_`.

### nfpms.name_template

> since 2019-11-15, removed 2020-04-14 (v0.132.0)

The `name_template` field was deprecated in favor of a more clear one,
`file_name_template`.

=== "Before"
    ``` yaml
    nfpms:
    - name_template: foo
    ```


=== "After"
    ``` yaml
    nfpms:
    - file_name_template: foo
    ```

### blob

> since 2019-08-02, removed 2020-03-22 (v0.130.0)

Blob was deprecated in favor of its plural form.
It was already accepting multiple inputs, but its pluralized now so its more
clear.

=== "Before"
    ```yaml
    blob:
      # etc
    ```

=== "After"
    ```yaml
    blobs:
      # etc
    ```

### sign

> since 2019-07-20, removed 2020-03-22 (v0.130.0)

Sign was deprecated in favor of its plural form.

=== "Before"
    ```yaml
    sign:
      # etc
    ```

=== "After"
    ```yaml
    signs:
      -
        # etc
    ```

### brew

> since 2019-06-09, removed 2020-01-26 (v0.125.0)

Brew was deprecated in favor of its plural form.

Change this:

=== "Before"
    ```yaml
    brew:
      # etc
    ```

=== "After"
    ```yaml
    brews:
      -
        # etc
    ```

### s3

> since 2019-06-09, removed 2020-01-07 (v0.125.0)

S3 was deprecated in favor of the new `blob`, which supports S3, Azure Blob and
GCS.

=== "Before"
    ```yaml
    s3:
    -
      # etc
    ```

=== "After"
    ```yaml
    blobs:
    -
      provider: s3
      # etc
    ```

ACLs should be set on the bucket, the `acl` option does not exist anymore.

### archive

> since 2019-04-16, removed 2019-12-27 (v0.124.0)

We now allow multiple archives, so the `archive` statement will be removed.

=== "Before"
    ```yaml
    archive:
      format: zip
    ```

=== "After"
    ```yaml
    archives:
      - id: foo
        format: zip
    ```

### snapcraft

> since 2019-05-27, removed 2019-12-27 (v0.124.0)

We now allow multiple Snapcraft configs, so the `snapcraft` statement will be removed.

=== "Before"
    ```yaml
    snapcraft:
      publish: true
      # ...
    ```

=== "After"
    ```yaml
    snapcrafts:
      -
        publish: true
        # ...
    ```

### nfpm

> since 2019-05-07, removed 2019-12-27 (v0.124.0)

We now allow multiple NFPM config, so the `nfpm` statement will be removed.

=== "Before"
    ```yaml
    nfpm:
      formats:
        - deb
    ```

=== "After"
    ```yaml
    nfpms:
      -
        formats:
          - deb
    ```

### docker.binary

> since 2018-10-01, removed 2019-08-02 (v0.114.0)

You can now create a Docker image with multiple binaries.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      binary: foo
    ```

=== "After"
    ```yaml
    dockers:
    - image: foo/bar
      binaries:
      - foo
    ```

### docker.image

> since 2018-10-20, removed 2019-08-02 (v0.114.0)

This property was deprecated in favor of more flexible `image_templates`.
The idea is to be able to define several images and tags using templates instead of just one image with tag templates.
This flexibility allows images to be pushed to multiple registries.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      tag_templates:
        - '{{ .Tag }}'
    ```

=== "After"
    ```yaml
    dockers:
    - image_templates:
        - 'foo/bar:{{ .Tag }}'
    ```

### docker.tag_templates

> since 2018-10-20, removed 2019-08-02 (v0.114.0)

This property was deprecated in favor of more flexible `image_templates`.
The idea is to be able to define several images and tags using templates instead of just one image with tag templates.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      tag_templates:
        - '{{ .Tag }}'
    ```

=== "After"
    ```yaml
    dockers:
    - image_templates:
        - 'foo/bar:{{ .Tag }}'
    ```

### git.short_hash

> since 2018-10-03, removed 2019-01-19 (v0.98.0)

This property was being used to tell GoReleaser to use short git hashes
instead of the full ones. This has been removed in favor of specific
template variables (`.FullCommit` and `.ShortCommit`).

=== "Before"
    ```yaml
    git:
      short_hash: true

    fake:
      foo_template: 'blah {{ .Commit }}'
    ```

=== "After"
    ```yaml
    fake:
      foo_template: 'blah {{ .ShortCommit }}'
    ```

### fpm

> since 2018-02-17, removed 2017-08-15 (v0.83.0)

FPM is deprecated in favor of nfpm, which is a simpler alternative written
in Go. The objective is to remove the ruby dependency thus simplify the
CI/CD pipelines.

Just replace the `fpm` keyword by `nfpm` in your `.goreleaser.yaml` file.

=== "Before"
    ```yaml
    fpm:
      # ...
    ```

=== "After"
    ```yaml
    nfpm:
      # ...
    ```

### docker.tag_template

> since 2018-01-19, removed 2017-08-15 (v0.83.0)

This property was deprecated in favor of the pluralized `tag_templates`.
The idea is to be able to define several tags instead of just one.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      tag_template: '{{ .Tag }}'
    ```

=== "After"
    ```yaml
    dockers:
    - image: foo/bar
      tag_templates:
        - '{{ .Tag }}'
    ```

### docker.latest

> since 2018-01-19, removed 2017-08-15 (v0.83.0)

The `latest` field in Docker config is deprecated in favor of the newer
`tag_templates` field.

=== "Before"
    ```yaml
    dockers:
    - image: foo/bar
      latest: true
    ```

=== "After"
    ```yaml
    dockers:
    - image: foo/bar
      tag_templates:
        - '{{ .Tag }}'
        - latest
    ```
