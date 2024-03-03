# Create a dev container in your GitHub Codespace including the Azure CLI and Terraform

Almost from scratch, I would like to describe the necessary steps for creating a dev container, which includes the Azure CLI and Terraform.

## Create a Codespace using the provided configuration files

To create a new Codespace, I’ll click on the “Remote Explorer” icon in Visual Studio Code, then I’ll switch to “GitHub Codespace”. Next I have to click on the “+” button:

<p align="center">
  <img src="pictures/06_create_new_cs.png" width="40%" height="30%" title="create_new_cs">
</p>

Now I’ll select the repository that I want to use for the Codespace:

<p align="center">
  <img src="pictures/07_create_new_cs_select_repo.png" width="30%" height="20%" title="create_new_cs_select_repo">
</p>

As the last step, I’ll choose which instance I would like to use. I’ll choose the 2 cores option:

<p align="center">
  <img src="pictures/07_create_new_cs_select_instance.png" width="60%" height="40%" title="07_create_new_cs_select_instance">
</p>

After that, the Codespace will be created:

<p align="center">
  <img src="pictures/08_building_dev_container.png" width="70%" height="50%" title="08_building_dev_container">
</p>

After the successful creation, I can recognize that an active Codespace is available for my repository:

<p align="center">
  <img src="pictures/09_git_repo_cs.png" width="60%" height="40%" title="09_git_repo_cs">
</p>

That is the view in Visual Studio Code:

<p align="center">
  <img src="pictures/10_finished_cs.png" width="60%" height="40%" title="10_finished_cs">
</p>
