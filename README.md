# Quantized Poro34B on VertexAI GCP
This repository includes instructions and files to run the quantized Poro-34B-GPTQ LLM model on GCP (with GPU). The Poro model card is here https://huggingface.co/LumiOpen/Poro-34B and the quantized model in here https://huggingface.co/TheBloke/Poro-34B-GPTQ.

### VertexAI and Instance setup

We assume that GCP billing has been set and a GCP project has been created. Navigate to the VertexAI home page and the Workbench tab. Create a new User-Managed Notebooks.

![Näyttökuva 2024-2-19 kello 11 39 17](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/4c3cbcf9-a7f3-473f-997c-3f1805c0d73c)

Select the region and zone, where you can spin up a VM with 40 GB GPU. And then press Continue.

![Näyttökuva 2024-2-19 kello 11 41 13](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/79a02967-3730-4820-b57f-baee8448a2f4)

Select Operating system "Debian 11" and Environment "Python 3 (with Intel MKL and CUDA 11.8)", and then press Continue.

![Näyttökuva 2024-2-19 kello 11 39 53](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/c70aaff6-0746-4b72-8512-03490c332f2e)

Choose "GPUs" and a GPU type "NVIDIA L4" and Number of GPUs "2". According to GCP's policies, a normal end-user can run maximum one GPU in one region. Typically NVIDIA GPUs have memory from 16 GB to 24 GB. However, this is not enough to run the quantized model. In order to run 2 or more GPUs on GCP, you need to make a quota request to one region (GCP screen "Quota increase requests", and for example, make a request of quota "NVIDIA L4 GPUs" from 1 to 2. The approval can take 1-2 business days. Choose the area that is closest to you or has extra capacity.) Machine type will automatically change to "g2-standard-24 (24 vCPU, 12 core, 96 GB memory)". Press Create.

![Näyttökuva 2024-2-19 kello 11 40 23](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/2de33912-3ed8-498f-936a-be50cf59343f)

After a while, an instance has been created. 

![Näyttökuva 2024-2-19 kello 11 45 28](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/e49b6c8e-947f-4811-9be7-477e60f33594)

Press "Open Jupyterlab" and the following screen will show up.

![Näyttökuva 2024-2-19 kello 11 46 18](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/87c023e3-7c40-4382-879d-f93e9cac695a)

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

![Näyttökuva 2024-2-19 kello 11 55 30](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/d71bb467-7755-4081-857f-332798ab66a6)

When the notebook is open, select the newly created "Poro" kernel using File -> Change Kernel -> Select Kernel Poro.

Now we are ready to execure the cells and test the Poro LLM model.

![Näyttökuva 2024-2-21 kello 15 54 04](https://github.com/MLConvexAI/Poro-on-GCP/assets/49635441/61f42fae-6b1d-4b93-aa99-e2e08abde9bf)





