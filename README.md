# Restaurant Bot

This example includes a file called `run.py`, which contains an example
of how to use Rasa directly from your python code.

## What’s inside this example?

This example contains some training data and the main files needed to build an 
assistant on your local machine. The `restaurantbot` consists of the following files:

- **data/nlu.md** contains training examples for the NLU model  
- **data/stories.md** contains training stories for the Core model  
- **actions.py** contains some custom actions
- **config.yml** contains the model configuration
- **domain.yml** contains the domain of the assistant  
- **endpoints.yml** contains the webhook configuration for the custom action  
- **policy.py** contains a custom policy
- **run.py** contains code to train a Rasa model and use it to parse some text

## How to use this example?
Adapted with https://github.com/RasaHQ/tutorial-rasa-alexa/blob/master/alexa_connector.py.  
To train your restaurant bot, execute
```
rasa train
```
This will store a zipped model file in `models/`.

To chat with the bot on the command line, run
```
rasa shell
```

Or you can start an action server plus a Rasa server by
```
rasa run actions
rasa run -m models --endpoints endpoints.yml
```

For more information about the individual commands, please check out our 
[documentation](http://rasa.com/docs/rasa/user-guide/command-line-interface/).

## Encountered any issues?
Let us know about it by posting on [Rasa Community Forum](https://forum.rasa.com)!

#### Troubleshooting
If you experience any issue during the installation of Rasa, make sure that you have python 3.7.x installed. Python 3.8.x on Mac is not compatible with tensorflow yet.
If while running 
```bash
rasa train
```

If you see the following error
```bash
File "/usr/local/Cellar/python/3.6.5_1/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages/questionary/constants.py", line 40, in <module>
    ('instruction', '')   # user instructions for select, rawselect, checkbox
TypeError: object() takes no parameters
```
Make sure you have installed the right package version and verify that your last installation of Rasa is pointing to the appropriate python environment. To check to what is pointing Rasa run
```bash
which rasa
```
Assuming it returns /usr/local/bin/rasa then do the following 
```bash
cat /usr/local/bin/rasa
```
The first line specifies the reference python environment. Verify that it matches the active virtualenv. An example of the output of cat might be:
```bash
#!/Users/gt/VirtualEnvironments/vui_core_2/bin/python3.6

# -*- coding: utf-8 -*-
import re
import sys

from rasa.__main__ import main

if __name__ == '__main__':
    sys.argv[0] = re.sub(r'(-script\.pyw?|\.exe)?$', '', sys.argv[0])
    sys.exit(main())
```
In my case it was wrong and I had to add the following line at the beginning
```bash
#!/Users/gt/.pyenv/shims/python
```