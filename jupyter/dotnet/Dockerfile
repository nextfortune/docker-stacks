FROM nextbiteam/jupyterlab-general:3.1.8-python3.8

User root
#Enable Microsoft PPA
RUN sudo -E wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb &&\
    sudo dpkg -i packages-microsoft-prod.deb

#Install dotnet sdk version 3.1
RUN sudo -E apt update &&\
    sudo -E apt install apt-transport-https &&\
    sudo -E apt install dotnet-sdk-3.1 -y

#Install dotnet tool dotnet interactive to install jupyter kernalspec of C#
RUN dotnet tool install --tool-path /usr/bin Microsoft.dotnet-interactive --version 1.0.155302 &&\
    dotnet interactive jupyter install

#chmod .local for jupyter start permission
RUN sudo chmod -R 777 .local
