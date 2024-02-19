# Quantized Poro34B on VertexAI GCP
This repository includes instructions and files to run the quantized Poro-34B-GPTQ LLM model on GCP (with GPU).

### VertexAI and Instance setup

We assume that GCP billing has been set and a GCP project has been created. Navigate to the VertexAI home page and the Workbench tab. Create a new User-Managed Notebooks.

![Näyttökuva 2024-2-19 kello 11 39 17](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/8807a8bc-3f09-4f13-9f30-8c5e1f1d1780)

Select the region and zone, where you can spin up a VM with 40 GB GPU. And then press Continue.

![Näyttökuva 2024-2-19 kello 11 41 13](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/12dd26d4-b068-4866-bd88-10ec707e7849)

Select Operating system "Debian 11" and Environment "Python 3 (with Intel MKL and CUDA 11.8)", and then press Continue.

![Näyttökuva 2024-2-19 kello 11 39 53](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/801ad8cc-0f69-48b4-9fa8-36780df4dee6)

Choose "GPUs" and a GPU type "NVIDIA L4" and Number of GPUs "2". According to GCP's policies, a normal end-user can run maximum one GPU in one region. Typically NVIDIA GPUs have memory from 16 GB to 24 GB. However, this is not enough to run the quantized model. In order to run 2 or more GPUs on GCP, you need to make a quota request to one region (GCP screen "Quota increase requests", and for example, make a request of quota "NVIDIA L4 GPUs" from 1 to 2. The approval can take 1-2 business days. Choose the area that is closest to you or has extra capacity.) Machine type will automatically change to "g2-standard-24 (24 vCPU, 12 core, 96 GB memory)". Press Create.

![Näyttökuva 2024-2-19 kello 11 40 23](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/22005886-33bc-4b5b-8a6a-d7ee6c028fa1)

After a while, an instance has been created. 

![Näyttökuva 2024-2-19 kello 11 45 28](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/ed183619-11c6-4925-9d0a-eadc74534376)

Press "Open Jupyterlab" and the following screen will show up.

![Näyttökuva 2024-2-19 kello 11 46 18](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/d89fcdfc-6d26-4d30-b9d4-45b47d07e266)

Press the "Terminal" icon, and a Terminal window will open. In this window, execute the following commands:

### Clone the repository
$ git clone https://github.com/MLConvexAI/Poro-on-GCP.git

### Update and install some libraries 

$ sudo apt-get update <br>
$ sudo apt install libcairo2-dev pkg-config python3-dev

### Create and Activate a Conda enviroment

$ conda create -n Poro <br>
$ conda activate Poro

### Install python libraries

$ cd Poro-on-GCP/  <br>
$ pip install -r requirements.txt <br>
$ PATH=$PATH:/home/jupyter/.local/bin

### Set up a new Kernel

$ python3 -m ipykernel install --user --name=Poro <br>

## Run the Poro notebook

Next navigate to Poro-on-GCP directory and open the Poro-34B-GPTQ-on-GCP notebook.

![Näyttökuva 2024-2-19 kello 11 55 30](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/7c9046e8-7494-4b4a-90fd-aff9e8f08893)

When the notebook is open, select the newly created "Poro" kernel using File -> Change Kernel -> Select Kernel Poro.

Now we are ready to execture the cells and test the Poro LLM model.



