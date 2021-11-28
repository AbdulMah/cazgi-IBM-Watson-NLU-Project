# coding-project-template
Install Server-side packages

    Change to the server directory.

    cd /home/project/cazgi-IBM-Watson-NLU-Project/sentimentAnalyzeServer

    All packages are needed to be installed are listed in package.json. Run npm install -s, to install and save those packages.

    npm install  -s

💡Click here for the checklist of required packages

    Run the server using the following command.

    npm start

    If all the required packages are successfully installed, the server should start without any issues.

    Press Ctrl+C to stop the server.

Part C: Install IBM Watson package and set up the .env file

    Install the ibm-watson package in your server side using the following command.

    npm install  -s ibm-watson@6.1.1

    Right click on the sentimentAnalyzeServer in the explorer and a new file named .env.

    Copy the credentials to point to your Watson NLU credentials from the IBM cloud, if you have not already done so in the previous lab.

    Add the credentials required to the .env file you created.

    The contents of the .env file would be as below

    API_KEY=<your api key>
    API_URL=<your url>

    Install dotenv to use the .env file in the server application using the following command.

    npm install  -s dotenv@10.0.0

    Make changes in your express JS (in the file named sentimentAnalyzerServer.js) to define and implement a method getNLUInstance() where you create an instance of NaturalLanguageUnderstanding using the credential from the .env file using dotenv package and return the instance. You can refer to this link for more details on how to do this.

    const NaturalLanguageUnderstandingV1 = require('ibm-watson/natural-language-understanding/v1');
    const { IamAuthenticator } = require('ibm-watson/auth');

    const naturalLanguageUnderstanding = new NaturalLanguageUnderstandingV1({
        version: '2021-08-01',
        authenticator: new IamAuthenticator ({
            apikey: api_key
        }),
        serviceUrl: api_url
    });
    return naturalLanguageUnderstanding;

Part D: Create end points

    Observe that the server code intends to provide 4 end-points. One of the end-points has been provided for you. Uncomment it and observe the code. It is highly recommended that you attempt to implement these end-points by yourself in sentimentAnalyzerServer.js before you use the code given below to complete the assignment.

    These are points you should keep in mind, while implementing the end-points.

    Each of the end points should use the getNLUInstance() created in the previous part to return appropriate response.
    Each end point should send a JSON or a string response as may be considered relevant.
    The JSON object returned from the IBM NaturalLanguageUnderstanding API is as in the below image. We need to extract the information that we need.

    /url/emotion end-point is used to analyze the emotion using NLU, for a given url.

    app.get("/url/emotion", (req,res) => {
        let urlToAnalyze = req.query.url
        const analyzeParams = 
        {
            "url": urlToAnalyze,
            "features": {
                "keywords": {
                    "emotion": true,
                    "limit": 1
                }
            }
        }
        
        const naturalLanguageUnderstanding = getNLUInstance();
        
        naturalLanguageUnderstanding.analyze(analyzeParams)
        .then(analysisResults => {
            //Retrieve the emotion and return it as a formatted string
            return res.send(analysisResults.result.keywords[0].emotion,null,2);
        })
        .catch(err => {
            return res.send("Could not do desired operation "+err);
        });
    });

    /url/sentiment end-point is used to analyze the sentiment using NLU, for a given url.

    app.get("/url/sentiment", (req,res) => {
        let urlToAnalyze = req.query.url
        const analyzeParams = 
        {
            "url": urlToAnalyze,
            "features": {
                "keywords": {
                    "sentiment": true,
                    "limit": 1
                }
            }
        }
        
        const naturalLanguageUnderstanding = getNLUInstance();
        
        naturalLanguageUnderstanding.analyze(analyzeParams)
        .then(analysisResults => {
            //Retrieve the sentiment and return it as a formatted string

            return res.send(analysisResults.result.keywords[0].sentiment,null,2);
        })
        .catch(err => {
            return res.send("Could not do desired operation "+err);
        });
    });

    /text/emotion end-point is used to analyze the emotion using NLU, for a given text.

    app.get("/text/emotion", (req,res) => {
        let textToAnalyze = req.query.text
        const analyzeParams = 
        {
            "text": textToAnalyze,
            "features": {
                "keywords": {
                    "emotion": true,
                    "limit": 1
                }
            }
        }
        
        const naturalLanguageUnderstanding = getNLUInstance();
        
        naturalLanguageUnderstanding.analyze(analyzeParams)
        .then(analysisResults => {
            //Retrieve the emotion and return it as a formatted string

            return res.send(analysisResults.result.keywords[0].emotion,null,2);
        })
        .catch(err => {
            return res.send("Could not do desired operation "+err);
        });
    });

    /text/sentiment end-point is used to analyze the sentiment using NLU, for a given text.

    app.get("/text/sentiment", (req,res) => {
        let textToAnalyze = req.query.text
        const analyzeParams = 
        {
            "text": textToAnalyze,
            "features": {
                "keywords": {
                    "sentiment": true,
                    "limit": 1
                }
            }
        }
        
        const naturalLanguageUnderstanding = getNLUInstance();
        
        naturalLanguageUnderstanding.analyze(analyzeParams)
        .then(analysisResults => {
            //Retrieve the sentiment and return it as a formatted string

            return res.send(analysisResults.result.keywords[0].sentiment,null,2);
        })
        .catch(err => {
            return res.send("Could not do desired operation "+err);
        });
    });

Part E - React Client Side

    Change to client directory sentimentAnalyzeClient.

    cd /home/project/cazgi-IBM-Watson-NLU-Project/sentimentAnalyzeClient

    All packages are needed to be installed are listed in package.json. To install and save those packages, run the following command in the terminal.

    npm install -s

    Make changes to client code

        Open the client code cazgi-IBM-Watson-NLU-Project/sentimentAnalyzeClient/src/App.js in the explorer

        Make changes to change the title of the page to "Sentiment Analyzer"

        Make changes to change the color of the sentiment response to green if the sentiment is positive, yellow if the sentiment is neutral and red if the sentiment is negative.

        Make changes in the cazgi-IBM-Watson-NLU-Project/sentimentAnalyzeClient/src/EmotionTable.js to use map function that we used in the Hands-on-ReactLab, to render the EmotionTable component as a below.
    💡Click here to see how to implement Map

    Run npm run-script build. Please note this is customized in package.json to generate and copy the client code to the server.

    Change to the server side.

    cd /home/project/cazgi-IBM-Watson-NLU-Project/sentimentAnalyzeServer

    Run the server. This will start on port 8080.

    npm start

    Connect to port 8080 from launch application. Verify your output on the browser. The output depending on which whether you choose text or URL and whether you choose sentiment or emotions, the output should vary.

    Please refer to this lab Working with git in the Theia lab environment

Part F: Commit and push your local code to your remote git repository

    In the terminal, go to the project directory.

    cd /home/project/cazgi-IBM-Watson-NLU-Project

    Please refer to this lab Working with git in the Theia lab environment

    Run the following command to add all the files to the remote repository. Remove the files that you have not changed from this list. Add any new files you have added to the list

    git add sentimentAnalyzeServer/package.json sentimentAnalyzeServer/package-lock.json sentimentAnalyzeServer/sentimentAnalyzerServer.js sentimentAnalyzeClient/src/App.js sentimentAnalyzeClient/src/EmotionTable.js

    Run the following command to commit your changes. Remove the files that you have not changed from this list. Add any new files you have added to the list

    git commit -m"Server and client side changes to implement the final project requirements" sentimentAnalyzeServer/package.json sentimentAnalyzeServer/package-lock.json sentimentAnalyzeServer/sentimentAnalyzerServer.js sentimentAnalyzeClient/src/App.js sentimentAnalyzeClient/src/EmotionTable.js

    Run the following command. You will be prompted by git for your username and password.

      `git push`

    Type your GitHub username and enter the personal access token you generated, for password. When you are authenticated, all committed changes are synced with your GitHub repository.

    Share the URL of your Git repository with all the changes. Ensure that the .env file with all the credentials is not added to the gitrepository.

Checklist for completion

    Client-side changes done as per requirements.
        Title changed to Sentiment Analyzer
        Changed the color of the sentiments
        Display response for emotion as a table

    Client side npm run-script build is run to build the client code and copy it to server side.

    .env file is created on the server side and the NLU credentials are added.

    All the four API endpoints have been implemented in the server side.

    Testing done from server side to see if the client is rendered as expected - Text Emotion, Text Sentiment, URL Emotions and URL Sentiment return results as expected.

    Code is pushed to Github.

Next step

The next and the final step is the deployment of the application on cloud foundry.
Author(s)

Lavanya
Other contributors

Upkar Lidder
Changelog
Date 	Version 	Changed by 	Change Description
2021-10-07 	0.4 	Sourabh 	Updated Git push instructions
2021-01-20 	0.3 	Lavanya 	Included npm version update
2021-01-20 	0.2 	Lavanya 	Included git login commands
2020-12-01 	0.1 	Lavanya 	Initial version created
			
© IBM Corporation 2020. All rights reserved.
