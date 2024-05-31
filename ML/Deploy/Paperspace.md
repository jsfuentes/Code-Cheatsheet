# Paperspace

Cloud GPUs as cheap as .47/hr

## Setup Script

Run:

```bash
#install asdf
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.11.2
```

Then add the following to .bashrc

```bash
. "$HOME/.asdf/asdf.sh"
. "$HOME/.asdf/completions/asdf.bash"
```

Then run:

```bash
asdf plugin-add python
```

## For Wav2Lip

```bash
mkdir Projects
cd Projects
git clone https://github.com/Rudrabha/Wav2Lip.git
asdf install python 3.6.12
asdf global python 3.6.12
sudo apt-get install ffmpeg
python3 -m venv venv
source venv/bin/activate

curl https://www.adrianbulat.com/downloads/python-fan/s3fd-619a316812.pth --output face_detection/detection/sfd/s3fd.pth
```

