### instalar pyenv

sudo dnf install -y gcc zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel \
    openssl-devel tk-devel libffi-devel


git clone https://github.com/pyenv/pyenv.git ~/.pyenv


echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init --path)"' >> ~/.bashrc

source ~/.bashrc


pyenv --version


pyenv install --list



### crea una version de python

pyenv install 3.6

pyenv global 3.11.9

python -m venv myenv

pip freeze > requirements.txt

pip install -r requirements.txt