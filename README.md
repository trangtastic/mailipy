<p align="center">
   <img width="120" alt="Mailipy Logo" src="./logo.png" />
</p>

# Mailipy

This is a software to make the task of sending bulk emails to a list of contacts
easier.

## Installation

    $ python3 -m venv path/to/venv
    $ source path/to/venv/bin/activate
    $ python3 -m pip install mailipy

In order to send emails, you need to first **generate** them and later **send**
them.

## Generating emails

You need to prepare a `template.md` file which must have a _YAML front matter_
(similarly to [what you find in
Jekyll](https://jekyllrb.com/docs/front-matter/)). See the example for the
keywords required in the front matter.

The command to create the emails is the following:

    $ mailipy-gen template.md contacts.csv

This will create as many emails as there are records in `contacts.csv`. The
emails will be stored in `outbox/` by default. You can use a third parameter to
change the outbox destination folder.

## Sending emails

Once you created the emails, run the following command (changing the outbox
directory accordingly):

    $ mailipy-send securesmtp.t-online.de:465 john.doe@magenta.de outbox
    $ mailipy-send smtp.gmail.com:465 john.doe@gmail.com outbox

The command will inform you of how many emails are going to be sent, and then
will prompt you for a password.

# Contributing

You can make changes to the [`gen.py`](./mailipy/gen.py) and
[`send.py`](./mailipy/send.py) scripts, and test these changes by running a
local version of Mailipy. After testing your changes, you can open a pull
request.

## Running a local version of Mailipy

1. Make sure you have [poetry](https://python-poetry.org/) installed in your
   system.
2. Run `poetry install` followed by `poetry shell` from the root of the source
   directory.
4. Now you can run `mailipy-gen` and `mailipy-send`, and these will include your
   local changes. You can verify that you're running a different binary than the
   globally installed one by running `which mailipy-gen`: the command will
   return the full path of the binary you're using.

## Running tests

After installing with `poetry install` and entering the `poetry shell`, run the
following:

    $ pytest

The command will search recursively for files named `*_test.py` and run them.
See the [pytest documentation](https://docs.pytest.org/en/latest/contents.html).
