# FHNW School of Business Onboarding Process #

Authors: Fabian Feiler, Lia Flück, Daniel Horn, Puneeth Krishna Suresh, Daniel Werner

digibp-monterosa


## Introduction ##


### Motivation ###

All students of the FHNW School of Business have gone through one big decision. What is the optimal degree program for one's interests, skills and career prospectives? What are the differences and specialities of the different programs? What are the basic criteria for a program? Many students have given feedback that they wish more support of these decisions from the school. The sub-process **Recommend Study Program** of the overall **FHNW School of Business Onboarding Process** solve this problem by providing a digitised workflow that leads students interactively through finding the answers to this questions.

As one of the group members of the digibp-monterosa team works for the FHNW School of Business and is the project manager of the digitalisation project of the sub-process **program registration** this is the perfect opportunity to introduce the new sub-process **Recommend study program**.


### Vision ###

Vision:

Matching a prospective student with the best fitting study program to foster the potential and satisfaction for students, study program, class environment and, therefore, as a consequence the society in economic and cultural aspects.


### Project Organisation ###

The project **digitalization of the FHNW School of Business Onboarding Process** is split into two sub-projects. The program registration project is managed within th FHNW School of Business organization. Its planned go-live is in spring 2019 and includes an online registration of the pogram through the tool ONLA that closely connected to EVENTO, the schools students management system. The sub-project **recommend study program** is implemented within the module **Digitalization of Business Processes** within the MSc Business Information Systems program. The project goal is the implementation of a workflow management system that supports students to decide for a study program that matches their skills and preferences. This sub-project is implemented within the spring semester 2018. In the following project overview the outline of the sub-project is shown. The implementation of certain parts go in line with the lectures in the module. 

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Organisation.PNG)


## Process ##
### Process Description ###

The overall process that is digitised within this module is the **FHNW School of Business Onboarding Process**. 
This process includes two sub-processes, the **Recommend Study Program process** and the **Program Registration Process**. 
As the **Program Registration process** is being digitised within an ongoing project by the School of Business, 
the main focus in this module lies on the **Recommend Study Program process**.

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Processes.PNG)


The FHNW school of Business Onboarding Process leads potential students of the School of Business from the first interest in being a student to the actual admission in a program (in a first step only BSc programs). In the sub-process **Recommend Study Program process**, the interested person is supported in choosing a program that matches his/her skills, interests and life-style. Also, the person can then participate in tests that enforce his/her choice. As soon as the interested person decides to register for the recommended program, the second sub-process, the **Program Registration process**, is triggered. 

Sub-Process: **Recommend Study Program Process**
- Process Goals: Support prospective students in their program decision, eliminate programs from the choice that do not meet the basic requirment for the person (does not meet language requirement, does not meet requirement for full-time/part-time program), 
- Inputs: form "Possbility Questionnaire", form "Recommendation Questionnaire", discretionary tasks (Loop) "Skills Tests"
- Outputs: List of possible programs, list of program recommendations, test results

Sub-Process: **Program Registration**
- Process Goals: Registration for program, check eligibility, payment of registration fee, add profile to EVENTO, discretionary task: interview
- Inputs: form "Program Registration", submit required documents (not digital), registration fee payment
- Outputs: program registration


"Recommend Study Program" as-is process:
Currently, there is only the sub-process "Program Registration" existant. There is no support for prospective students to decide for a program. As the overall onboarding process is going through some changes and digitalization efforts, this is a good moment to re-design the process and add the sub-process of programm recommendations. 


Project "Recommend Study Programm":
The project for the digitalization of the sub-process "Recomend Study Program" is done within the Module "Digitalization of Business Processes" of the MSc Business Information Systems program. The goal is to digitise the process through a workflow management system with some service integration.


### Process Modell ###

The following picture illustrates the complete designed process:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Process_Camunda.png)

The process starts with the prospective candidate, that visits the created wordpress-website and clicks on the study recommondation 
link. This link forwardes the user to the first google-form where 

#### Task Types ####
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Task_types.png)

#### Event Types ####
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/event_types.png)

#### User & Groups ####
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/User.png)



## Digitalisation ##
### DMN ###

Within the first process step according to the process model, a user is going to fill in a questionnaire. Based on the input data of this questionnaire and the [study regulation](https://www.fhnw.ch/de/studium/wirtschaft) a preselection of possible study programms is made by a DMN (Decision Model and Notation). The following DRD (Decision Requirement Diagram) shows the relation of the input data for the DMN.

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/DRD_BSc_program.png)

The determined business rules have been applied within a DMN in order to execute a preselection of a study program. The following DMN shows the determined business ruls.

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/DMN_BSc_program.png)

### Services ###

The following services habe been implemented into the process, but due to user friendliness, the ChatBot has not been connected. Instead Google Forms and Google Sheets have been conected to the process.

#### Google Forms / WordPress Website ####

As simple WordPress website has been created which serves as the starting point of the process (see [URL](https://programrecommendation.wordpress.com)). Google Forms has been linked with Responses in a Google Sheet (see next section). Therefore the link is available on the WordPress Website. Google sheets runs a script when the Google Form is submitted ([see script](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/txt/Google_Sheets_rest_API_camunda.txt)). The script triggers the process to be started. The fist Task in the process is a Service Task, sending an e-mail to the user with the camunda invitation link. 

#### Google Sheets ####

Within the process step fill in recommendaton questionnaire of the process model a user is going to fill in form. The data from this form is posted in a Google Sheets file. The objective of the Google sheet is to calculate the best match of a study programm. The following image shows a screenshot of the Google Sheet. 

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/excel.png)

Logic of the Google Sheet:
1. Camunda values are posted in column B [Questionnaire form data]
2. For each Bachelor program, an ideal questionnaire-response was defined in relation with program heads.
3. The prospective candidate’s questionnaire result is then compared to these pre-defined responses.
4. Ranking is based on “Olympic Medal-Model”:
     -	highest number of perfect matches
     -	in case of tie: higher number of only one deviation
     -	in case of tie: higher number of only two deviations
     -  and so on
     Same for second and third.
5. In the cells A36 to B38 an output containing the 3 best matches of study programs will be displayed.

#### ChatBot ####

An initial effort of providing a more personalized function is provided to capture the preliminary details using a chat bot. This scenario is realized using Dialog Flow and Integromat. The values are stored in Spreadsheet using web hooks.

A brief description of the concept used to realize this is depicted below:

- The Different Intents created and used to realize this Chat bot are shown below
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot1.png)

- The Chat bot is triggered when the candidates provides “hi” or “hello” as a greeting message and the flow of communication is passed to the next intent. The concept used in creating this is an inline intent within the context of the existing intent as shown below:
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot2.png)

- The entities in this case were Boolean values (yes or no), thus this example did not used any inbuilt entity and created four different entities for the Boolean values that we require.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot3.png)

- The value at each intent is captured and stored for that instance and passed on to the next so that at the end of the entire conversation, a combination of all captured values can be collected and passed on to Integromat for back end service integration (In our example a Google spreadsheet). An example of both the above-mentioned scenarios are shown below:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot4.png)

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot5.png)

-Since this example demonstrated an inline intent, it is not required to enable a web-hook to call for each intent. The web hooks need to be enabled in Dialog Flow where the values of all the intents (Ex: Last Intent) is being captured as shown below:
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot6.png)

- A scenario has to be created in integromat to capture the values from Dialog Flow and store it in the back end. This example demonstrates a simple example of web hooks and Google Spreadsheet as shown below:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot7.png)

- This has to be connected with Dialog Flow using a Web hooks URL and pasted in the Fulfilment stage of Dialog Flow.

- Once this step is completed and run for a demo, all values communicated and captured in the chat bot would be sent to the Web hooks and in turn to each individual row on Google Spreadsheet as shown below:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot8.png)

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot9.png)

### Integration ###

For the integration of the services Microsoft Flow and Integromat have been used.

#### Microsoft Flow ####

##### Microsoft Flow – POST: Sending of information e-mail

Microsoft flow has been used for sending an e-mail containing information concerning the study programm.

- Service Task REST with Body
- URL: [MS Flow HTML request]
- Method: POST
- Headers: Content-Type:application/json
- Payload: 

var email = execution.getVariable("email");
var out = {"email":email};
JSON.stringify(out);

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Post_sending_email.png)

[Link JSON-Request](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/txt/JSON_request_sending_mail.txt)

##### Microsoft Flow – POST: Sending of invitation e-mail

A e-mail is going to be send to the user containing the camunda invitation link.

- Service Task REST with Body
- URL: [MS Flow HTML request]
- Method: POST
- Headers: Content-Type:application/json
- Payload: 

var email = execution.getVariable("email");
var out = {"email":email};
JSON.stringify(out);

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/post_sending_email_invitation.png)

[Link JSON-Request](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/txt/JSON_request_sending_mail_invitation.txt)

##### Microsoft Flow – POST Questionnaire Data to Google Sheets

Microsoft Flow has been appllied in order to post the input data from the questionnaire to the Google Sheets.

- Service Task REST with Body
- URL: [MS Flow HTML request]
- Method: POST
- Headers: Content-Type:application/json
- Payload: form field variables


![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/MS_flow_1.png)
...
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/MS_flow_2.png)


JSON-Request to post the data looks as follow:

[Link JSON-Request](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/txt/JSON_request_MS_flow.txt)

#### Integromat ####

##### Integromat – GET program recommendation from Google Sheets 

Integromat has been appllied in order to get the study recommendation from Google Sheets.

- Service Task REST without Body
- URL: [Integromat webhook]
- Method: GET

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Integromat.png)

The JSON for request the data looks as follow:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Integromat_JSON.png)

The same applies for “second” and “third” program. Both invoked separately by an own integromat scenario.

## Step by step Instruction ##

1. Open following files in [this folder](https://github.com/DigiBP/digibp-monterosa/tree/master/src/main/resources/modelling) with the Camunda Modeler:
   - DMN_BSc program_180524.dmn
   - onboarding_180528.bpmn
   
2. Deploy both files within the Camunda Modler

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/1.deploy_process.gif)

3. Open [Heroku](http://heroku.com) and sign-in.

4. Go to "Deploy" and click on "Deploy Branch"

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/2.deploy_branch.png)

5. Open the app

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/3.OpenApp.png)

6. Log in to Camunda

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/4.LogInCamunda.png)

7. Start the process "Program recommendation module"

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/5.StartProcess.gif)

8. Fill in the form

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/6.form.gif)

9. Display results

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/7.DisplayRecommendation.gif)

10. Fill in recommendation questionnaire

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/9.Form2.gif)

11. Evalutation of results 

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/10.Evaluation.gif)

12. Show results

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/11.DisplayResult.gif)

13. Further procedure and end of process

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/12.FurtherProcedure.gif)

## Problems & Lessons Learned ##





