# Submission script for Realistic/Advanced Image Synthesis

## Requirements

The submission script relies on a few Python modules and the OpenEXR library. We provide instructions for Linux, macOS, and Windows, assuming you have access to [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/install-win10) on Windows 10. If you have problems running the script, please email the TAs or see them at their office hours. __Don't wait until the deadline to make sure this script works; test it beforehand!__

### Linux / WSL
```bash
sudo apt-get install libopenexr-dev  # OpenEXR library
sudo apt-get install python-pip      # Python package manager
```

### macOS

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  # Homebrew
brew install openexr                                # OpenEXR library
curl https://bootstrap.pypa.io/get-pip.py | python  # Python package manager
```

You can verify that `pip` is correctly installed by typing `pip` in the command-line. To install the requirements for the tools, run
```bash
pip install --user -r requirements.txt  # Install Python modules
```
You can check that all packages have been installed by typing `pip list`.

## Configuration file

Every assignment comes with a `config.json` file within the `data` directory of the basecode. Each field needs to be filled by the student, except the scene titles (`renders/scene` fields) which are already provided. Below is the sample config file to be modified.

```JSON
{
  "firstlast": "John Doe",
  "id": 123456789,
  "assignment": 1,
  "course": 446,
  "renders": [
    { "scene": "Veach Ajar",
      "render": "renders/veach_ajar.exr"
    },
    { "scene": "Living room",
      "render": "renders/living_room.exr"
    },
    { "scene": "Bathroom",
      "render": "renders/bathroom.exr"
    }
  ]
}
```

## Creating a submission

Once you are done generating all your images, make sure the paths in `config.json` are correct and simply run
```bash
python submit.py config.json
```

within the terminal. This script can take a few seconds to run depending on the tasks. Behind the curtains, `submit.py` essentially converts your OpenEXR images to PNG images, and then embeds them into an HTML template as base64 images. An horizontal slider is used to allow graders to easily compare your outputs with theirs (which you don't have access to, hence the broken link). Your student and assignment informations are parsed and put into an HTML file to be rendered by your browser.

The result is a standalone submission file `a1_123456789.html` containing all of your rendered images. Depending on the assignment, this file can be somewhat heavy since all your image data is contained within the file. __Make sure the output is correct before submitting your assignment!__

## Submission example

To see a sample submission, have a look at `sample.html`. Running the script with the default configuration file should yield a new submission which is identical to it.

## Converting from OpenEXR to PNG/JPG

An additional script is provided to convert a rendered image in OpenEXR format to PNG/JPG format. This code is part of `submit.py` but a standalone version is provided, if needed. To convert to PNG, run

```bash
python convert.py input.exr output.png
```
The output can also be a JPEG image; the script will automatically detect the output format.
