# fastai-binder-app-template
This is a template github project for building your binder app based on [Lesson 3 of the fastai course v4](https://course.fast.ai/videos/?lesson=3) (2020) and also discussed in [Chapter 2](https://github.com/fastai/fastbook/blob/master/02_production.ipynb) of the book **"Deep Learning for Coders with fastai and Pytorch"** . This template is based on the [instructions posted on the fastai forums here](https://forums.fast.ai/t/deploying-your-notebook-as-an-app-under-10-minutes/70621?u=butchland).

## Instructions for Deploying to Binder
_(Note that for Colab, see the [special instructions below](#special-instructions-for-colab) as it does not provide a terminal environment, nor does it run voila, and also does not persist your data across sessions)_

_Do the next steps only after making sure you already created and exported the learner (`export.pkl`) and your stripped down voila app notebook is ready (preferably tested in a jupyter notebook environment with voila)._

1. Create a [github account](https://github.com/join?source=header-home) if you don't have one yet.
1. Fork [this repo](https://github.com/butchland/fastai-binder-app-template) as a template for your own binder app repository. You can [click on this link to generate your own copy.](https://github.com/butchland/fastai-binder-app-template/generate) 
   * Make sure to rename your repo to something other than `fastai-binder-app-template`. Due to a github policy, `git-lfs` does not support uploads to public forks, which is what your repo will be if you name it the same as what you are copying from. For more info, please see [this issue](https://github.com/git-lfs/git-lfs/issues/1906). 
1. Clone your newly created repository into the machine running your jupyter notebook (which can be either your local machine, Colab, Paperspace Gradient notebooks or your GCP, Sagemaker and other VM instances)
    * If you are running the notebooks on a standard jupyter notebook environment (e.g. Paperspace Gradient), you can create a terminal to run your git and shell commands. _(For Colab, no terminal environment is provided, so see the [special instructions](#special-instructions-for-colab))_
    ![](https://raw.githubusercontent.com/butchland/fastai-binder-app-template/master/images/create-jupyter-terminal.png)
    * If `git` is not installed on your jupyter environment, install it by following [these instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
    * You might have to run the following commands to setup your email and username for `git`:
        * `git config --global user.name "<Your name>"`
        * `git config --global user.email "<email@address>"`
    * **[Optional]** In order to push code to a github repo, it is usually convenient to create an ssh key to authenticate yourself. See [instructions here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh) on creating an ssh key and registering it on github.
        * `ssh` is normally installed on Ubuntu and other Linux systems by default, but if it is not installed (e.g. Paperspace Gradient), you can install it by following [the instructions here](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/).
    * To clone your repo,run either of the following commands:
        *  _(Run this if you have already setup your ssh key)_
        
        `git clone git@github.com:/<your-github-id>/<your-copy-of-fastai-binder-app-template>.git` 

       
        * _(Run this if you haven't setup your ssh key,  but this will require you to input your github id and password each time you push your code)_
        
        `git clone https://github.com/<your-github-id>/<your-copy-of-fastai-binder-app-template>.git`

        
1. Copy over the following from your jupyter environment:
    * the `export.pkl` created in [Chapter 2](https://github.com/fastai/fastbook/blob/master/clean/02_production.ipynb) as the exported learner for classifying bear images
    * the stripped down notebook from [Chapter 2](https://github.com/fastai/fastbook/blob/master/clean/02_production.ipynb) containing only the voila app. 

    A [sample notebook](https://github.com/butchland/fastai-binder-app-template/blob/master/sample-fastai-binder-app.ipynb) is provided but stripping down the [Chapter 2 notebook](https://github.com/fastai/fastbook/blob/master/clean/02_production.ipynb) is a good exercise for building more voila apps in the future.
1. **[Optional]** Test your stripped down voila app notebook using voila in your jupyter environment.
1. Install `git lfs` on your local environment. If you are running on Jupyter notebook, create a terminal and run your installation commands there.  See [instructions here](https://github.com/git-lfs/git-lfs/wiki/Installation)
1. Push your code changes into your github repository. Run the following git commands:
    * `git add .`
    * `git commit -m 'Add my app notebook and exported learner'`
    * `git push`

    _Note: the `git push` command might take a while as it is uploading your `export.pkl` file_
1. Head over the [binder site](https://mybinder.org/) and  continue following the [instructions to run the app on binder](https://forums.fast.ai/t/deploying-your-notebook-as-an-app-under-10-minutes/70621?u=butchland). _Note that the `.gitattributes` and `requirements.txt` files have already been provided as part of this template repo._

_Note: just a slight modification to the instructions provided: In the field `Path to a notebook file (optional)`, change the path type from `File` to `URL`._


## Special Instructions for Colab

Because Colab uses a non-standard Jupyter environment, it is not as easy to run and test your voila app in Colab. You can however still build and export your learner to `export.pkl` and strip down your Chapter 2 notebook so that it will run on binder as a voila app.

The easiest way to setup your github repo is to clone it on Colab and add your exported learner (`export.pkl`) to your repo via `git` (with  `git lfs` installed).
You can add your stripped down notebook manually as detailed in the [instructions below](#adding-your-stripped-down-voila-app-notebook).

### Running git and shell commands
In order to run shell and git commands on Colab, you can create a new cell and
add a `%%bash` on the first line. You can then add any git or shell commands after the first line and execute it as a pseudo terminal.

* First, `cd` into your `/content` directory
```
%cd /content
```
* Install `git-lfs` by following the [instructions here](https://github.com/git-lfs/git-lfs/wiki/Installation)
* Clone your repo into your Colab VM
```
%%bash
git config --global user.name "<Your name>"
git config --global user.email "<email@address>"
git clone https://github.com/<your-github-id>/<your-copy-of-fastai-binder-app-template>.git
```
* cd into your local git repo
```
%cd <your-copy-of-fastai-binder-app-template>
```
* Add and commit your exported learner into your local repo
```
%%bash
cp ../export.pkl .
git add export.pkl
git commit -m "Add exported learner"
```

### Pushing your notebook to Github
Due to some weird limitations, Colab does not allow ssh access from your Colab VM to your github repo, thus requiring the use of 'https://github.com:...' format for pulling and pushing your git repo. 

The problem is that when trying to push your changes back, executing `git push` in a jupyter notebook cell triggers an error as well.

The solution is to use the `git credentials` command to store your credentials so that `git` will use the credentials without asking for a prompt (a prompt asking for your userid/password triggers an  error on Colab since we are not running these commands on a terminal)

* To configure `git` to use our stored credentials, we need to configure our local repo settings by running the following command
```
%%bash
git config credential.helper store
```
* Then we create a `.git-credentials` file in the home directory `/root` containing our github user id and password in the format `https://<github-userid>:<password>@github.com`

```
%%bash
echo "https:<github-userid>:<password>@github.com" > /root/.git-credentials
```

_Note that this is a **MASSIVE SECURITY HOLE** since your github password is stored in plain text. **Please delete both the cell containing this in the jupyter notebook as well as the `.git-credentials` file itself after you've pushed your changes.**._

* Run the `git push` command
```
%%bash
git push
```

Your github repo should now contain the exported learner (`export.pkl`).

### Adding your stripped down voila app notebook 

To add your voila notebook (which I assume will be in your `Google Drive` under the `Colab Notebooks` folder), you can save this stripped down voila notebook directly into  your Github repository by clicking on the `Save a copy in Github` option under the `File` menu option.

_(You might have to authorize Colab to access your github repositories the first time you do this)_. 

![](https://raw.githubusercontent.com/butchland/fastai-binder-app-template/master/images/colab-save-copy-in-github.png)

Please make sure to pick the right repository to save your stripped down voila notebook.

### Saving your repo and other files

Unfortunately, Colab is not your standard Jupyter environment and does not support voila natively so there is no easy way to test your stripped down voila notebook prior to deploying it on github repo and running on binder. 

_Note: As of 9/17/2020, the ipywidgets (including the image cleaner) are now runnable on Colab, just not the voila app._

Also, because Colab does not persist your VM instance storage across sessions, please connect your Google Drive and copy your downloaded data, your cloned repository and your exported learner (`export.pkl`). By default, your exported learner and your cloned repository will be created in the `/content` directory.

**Big thanks to [@vikbehal](https://forums.fast.ai/u/vikbehal) for providing the instructions!**

 
