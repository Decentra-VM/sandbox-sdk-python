Setting up the environment

With Rye

We use Rye to manage dependencies.
Rye automatically provisions a Python environment with the expected Python version.

To set it up run

scripts slash bootstrap

Or install Rye manually and run

rye sync all features

You can then run scripts using

rye run python script.py

Or activate the virtual environment

source dot venv slash bin slash activate

Now you can omit the rye run prefix

python script.py

Without Rye

If you do not want to install Rye you can use pip directly.

Ensure you have the Python version specified in dot python version.
Create a virtual environment.
Install dependencies using

pip install dash r requirements dev lock

Modifying or adding code

Most of the SDK is generated code.
Modifications will persist between generations.
Manual changes may cause merge conflicts with regenerated code.

The generator will never modify contents of
src slash sandbox underscore sdk slash lib
examples

Adding and running examples

Files in the examples directory are never modified by the generator.

Add an example file to

examples slash your example dot py

Make it executable

chmod plus x examples slash your example dot py

Run the example

dot slash examples slash your example dot py

Using the repository from source

You can install from git or link to a cloned repository.

Install via git

pip install git plus ssh colon slash slash git at github dot com slash avm dash codes slash sandbox dash sdk dash python dot git

Build from source

Building creates two files in dist
A source archive
A wheel file

Create a distributable version

rye build

Or

python dash m build

Install the wheel

pip install dot slash path dash to dash wheel dash file dot whl

Running tests

Most tests require a mock server based on the OpenAPI spec.

You will need npm installed.

Run a mock server

npx prism mock path slash to slash your slash openapi dot yml

Run tests

scripts slash test

Linting and formatting

This repository uses ruff and black.

To lint

scripts slash lint

To format and automatically fix ruff issues

scripts slash format

Publishing and releases

Changes made through the automated release pipeline publish to PyPI automatically.

If changes are made manually you may need to release manually.

Publish with GitHub workflow

Use the Publish PyPI GitHub action.
Requires repository or organization secrets.

Publish manually

Run the publish PyPI script with PYPI token set in the environment.
