**********************************
Managing GitHub labels with Python
**********************************

I've written a pretty quick and dirty script to ensure the expected labels exist in GitHub repositories.

I found a few variations on this via Google, but they seemed to be old and had issues (no pun intended!).

The script is in my [GitHub repository](https://github.com/peteGSX-Projects/manage-github-labels), and uses a personal access token along with a JSON formatted text file of label data to either create or update the required labels.

To use the script, you will need a recent version of Python 3 (written/tested with 3.10.6).

Once Python is installed, this is what you need to do:

- virtualenv venv
- venv/scripts/activate
- pip install -r requirements.txt

To run the script, you need to provide the owner or organisation name, repository name, a personal access token, and the name of the JSON file containing the label data. An example file is included in the repository.

.. code-block:: 

  python manage-github-labels.py -o <Owner/Organisation> -r <Repository> -t <Personal Access Token> -f labels.json

The format for the JSON file is as follows:

.. code-block:: json

  {
    "<Label name>": {
      "colour": "<Colour code in hex>",
      "description": "<Description>"
    }
  }

If the label does not exist, it will be created with the provided details.

If the label exists but does not match the provided details, it will be updated.

Once the labels in the JSON file are processed, any other labels in the repository will be listed at the command line.