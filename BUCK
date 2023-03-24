# Copyright 1999-2023. Plesk International GmbH. All rights reserved.
# vim:ft=python:

PRODUCT_VERSION = '0.1.0'

genrule(
    name = 'version',
    out = 'version.json',
    bash = r"""echo "{\"version\": \"%s\", \"revision\": \"`git rev-parse HEAD`\"}" > $OUT""" % (PRODUCT_VERSION),
)

python_library(
    name = 'actions.lib',
    srcs = glob(['./actions/*.py']),
)

python_library(
    name = 'common.lib',
    srcs = glob(['./common/*.py']),
)

python_library(
    name = 'libs.lib',
    srcs = glob(['main.py']),
    deps = [
        ':actions.lib',
        ':common.lib',
    ],
    resources = [
        ':version',
    ],
)

python_test(
    name = 'libs.tests',
    srcs = glob(['./tests/*.py']),
    deps = [
        ':common.lib',
        ':actions.lib',
    ],
    platform = 'py3',
)

python_binary(
    name = 'centos2alma',
    platform = 'py3',
    main_module = 'main',
    deps = [
        ':libs.lib',
    ]
)
