---
title: "Random Data Generator"
date: 2022-05-11T15:46:05-05:00
draft: false
weight: 115
---

## Description

During the development of the Linux curriculum we created a random data generator. The reason it was creaeted was to allow the learners work with tools like grep, sed, curl, and wget using a pre-defined data-set.

The generator allows users to do the following:
- Send a request to the api to receive a random data set
- Send a request to the api to receive a pre-defined data set
- Receive the dataset in CSV or JSON format 

## Examples

You can send curl requests to the following endpoints or simply enter the url into a new browser window:

The two requests below will return a json formatted document within your browser window
- `https://jwoolbright.com/api/walkthrough/user`
- `https://jwoolbright.com/api/exercise/sensitive`

The two requests below will simply download a CSV document of the data (most likely to your downloads folder)
- `https://jwoolbright.com/api/walkthrough/user?data_format=csv`
- `https://jwoolbright.com/api/exercise/sensitive?data_format=csv`

You can view the docs for the generator here: [Random Data Generator Docs](https://jwoolbright.com/api/docs)

You can find the github repository here: [Random Data Generator Github Repo](https://github.com/LaunchCodeTechnicalTraining/dummy-generator-api)
