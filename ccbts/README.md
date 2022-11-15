# CoCo Bot: Manipulate objects on a board!

This repository contains the source code for a collaborative CoCobot session. It can be run on the [slurk](https://github.com/clp-research/slurk) server. 


## Setting up and running

### Setup 

1. Install [Docker](https://docs.docker.com/get-docker/). You might also need the [jq package](https://stedolan.github.io/jq/download/) too. 
2. Clone the [slurk](https://github.com/clp-research/slurk) repository.
3. Copy the [```wordle.js```](wordle.js) file to [```slurk/slurk/views/static/plugins```](https://github.com/clp-research/slurk/tree/master/slurk/views/static/plugins). 
4. Before running the bot, several environmental variables would need to be generated and assigned. This process is detailed in the [documentation](https://clp-research.github.io/slurk/slurk_gettingstarted.html), which details both the general preparation and the [bot specific initialisations](https://clp-research.github.io/slurk/slurk_gettingstarted.html#chatting-with-a-bot). The bot also needs to have specific permissions, listed below this paragraph. The above permissions can be found in [this example permissions file](https://github.com/clp-research/slurk-bots/blob/ccbts/ccbts/data/bot_permissions.json) already.  
    ```
    {
        "api": true,
        "send_html_message": true,
        "send_privately": true,
        "send_command": true
    }
    ```
    **To skip all this setup above, you could run a [setup script](https://github.com/clp-research/slurk-bots/blob/ccbts/ccbts/setup.sh).** 
    1. Make sure that the [slurk](https://github.com/clp-research/slurk) and slurk-bots repositories live next to each other on the same level.
    2. Navigate to the base directory of this repository and run the script to launch this bot, your command should look like ```bash ccbts/setup.sh``` 
    This script will build and run the docker images, it will initialise all the env variables with the right permissions and it will set up two bots that can talk to each other locally on your computer. The bot will appear in your containers list as ```slurk/ccbts-bot```. At the end of the run there will be two tokens printed in the shell that you will need to paste to access the waiting rooms. 
5. Save the generated tokens!

Note: Every time a new terminal session is started, the env variables will need to be set up again. You can just run the script again. 
    
### Running and playing the bot

If you have everything already set up, you can run the bot using the following command (take notice of the right env variable names):    
```bash
docker run -e CCBTS_TOKEN=$THIS_BOT_TOKEN -e CCBTS_USER=$THIS_BOT -e CCBTS_TASK_ID=$TASK_ID -e SLURK_WAITING_ROOM=$WAITING_ROOM -e SLURK_PORT=5000 --net="host" slurk/ccbts-bot &
```

To access the waiting rooms, you will need to input the saved tokes as well as any string as username. If you ran the setup script, there will be two tokens towards the end that will look something like below. You could use one for each instance of the bots playing Wordle together. 
```
2f42a98e-0a29-43c2-9f94-97b38f25c30f
4cf0a403-c8d4-48fa-a7b0-b8ea7d52a364
```


## Modifications
Under `lib/config.py` you find a number of global variables that define experiment settings as well as short descriptions of their effect on the experiment.