﻿# Create a dev container in your GitHub Codespace including the Azure CLI and Terraform

Almost from scratch, I would like to describe the necessary steps for creating a dev container, which includes the Azure CLI and Terraform.

## Create a Codespace using the provided configuration files

To create a new Codespace, I’ll click on the “Remote Explorer” icon in Visual Studio Code, then I’ll switch to “GitHub Codespace”. Next I have to click on the “+” button:

<p align="left">
  <img src="pictures/06_create_new_cs.png" width="40%" height="30%" title="create_new_cs">
</p>

Now I’ll select the repository that I want to use for the Codespace:

<p align="left">
  <img src="pictures/07_create_new_cs_select_repo.png" width="30%" height="20%" title="create_new_cs_select_repo">
</p>

As the last step, I’ll choose which instance I would like to use. I’ll choose the 2 cores option:

<p align="left">
  <img src="pictures/07_create_new_cs_select_instance.png" width="60%" height="40%" title="07_create_new_cs_select_instance">
</p>

After that, the Codespace will be created:

<p align="left">
  <img src="pictures/08_building_dev_container.png" width="70%" height="50%" title="08_building_dev_container">
</p>

After the successful creation, I can recognize that an active Codespace is available for my repository:

<p align="left">
  <img src="pictures/09_git_repo_cs.png" width="80%" height="60%" title="09_git_repo_cs">
</p>

That is the view in Visual Studio Code:

<p align="left">
  <img src="pictures/10_finished_cs.png" width="80%" height="60%" title="10_finished_cs">
</p>

I’m going to verify that the desired tools are installed. Therefore, I’ll enter “az” in the terminal:

<p align="left">
  <img src="pictures/11_finished_cs_azure.png" width="80%" height="60%" title="11_finished_cs_azure">
</p>

In addition, I also prove that Terraform was provided properly by typing “terraform”:

<p align="left">
  <img src="pictures/12_finished_cs_terraform.png" width="80%" height="60%" title="12_finished_cs_terraform">
</p>

So my Codespace named “obscure funicular” is ready, which includes my customized dev container, and I would be ready to start my development using Terraform on Azure.

## Stop your Codespace

Don’t forget to stop the Codespace, if you don’t need it:

<p align="left">
  <img src="pictures/13_stop_cs.png" width="80%" height="60%" title="13_stop_cs">
</p>
