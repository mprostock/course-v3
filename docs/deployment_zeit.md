---
title: "Deploying on Zeit"
sidebar: home_sidebar
---

<img alt="" src="/images/zeit/zeit_now.png" class="screenshot">

This is quick guide to deploy your trained models using the [Now](https://zeit.co/now) service from [Zeit](https://zeit.co/).  This guide comes with a starter app deploying Jeremy's Bear Image Classification model form Lesson 2.

## One-time setup

### Install Now's CLI (Command Line Interface)

```bash
sudo apt install npm # if not already installed
sudo npm install -g now
```

### Grab starter pack for model deployment

```bash
wget https://github.com/fastai/course-v3/raw/master/docs/production/zeit.tgz
tar xf zeit.tgz
cd zeit
```

## Per-project setup

### Upload your trained model file

Upload your trained model file (for example `stage-2.pth`) to a cloud service like Google Drive or Dropbox. Copy the download link for the file. **Note:** the download link is the one which starts the file download directly&mdash;and is normally different than the share link which presents you with a view to download the file (use [https://rawdownload.now.sh/](https://rawdownload.now.sh/) if needed)

If you want to just test the deployment initially, you can use Jeremy's bear classification model from Lesson 2, you can skip this step, since that model's weights URL is already filled in the sample app.

### Customize the app for your model

1. Open up the file `server.py` inside the `app` directory and update the `model_file_url` variable with the url copied above
1. In the same file, update the line `classes = ['black', 'grizzly', 'teddys']` with the classes you are expecting from your model

### Deploy

On the terminal, make sure you are in the `zeit` directory, then type:

```bash
now
```

The first time you run this, it will prompt for your email address and create your Now account for you. After your account is created, run it again to deploy your project.

Copy the url that Now assigns the project (shown on the terminal right after the above command)&mdash;example `https://xxxxxxxxxx.now.sh`. **NB**: The URL is shown at the very top of the large amount of output, so you will need to scroll up to see it.

When the **deployment finishes** and it shows *"> Success! Deployment ready"* on the terminal, type in the terminal:

```
export URL='xxx'
export NAME='something-cool'
now alias $URL $NAME
now scale $NAME.now.sh sfo 1
```

(**Note:** replace `something-cool` above with some unique name that you choose, and `xxx` with the URL shown in the `now` output.)

### Test the URL of your working app

Go to `$NAME`.now.sh in your browser and test your app.

## Local testing

In case you want to run the app server locally, make these changes to the above steps:

Instead of

```bash
now
```

type in the terminal:

```bash
python app/server.py serve
```

Go to [http://localhost:5042/](http://localhost:5042/) to test your app.

---

*Thanks to Navjot Matharu for the initial version of this guide, and Simon Willison for sample code.*

