↰ [Return to Index](index.md)

# Urbit AArch64 APT Repository

If you're running a debian derivative, you can install Urbit as a debian package:

#### Import the repository signing key

`curl https://s3.us-east-2.amazonaws.com/urbit-on-arm/urbit-on-arm_public.gpg | sudo apt-key add -`

#### Add the repository to your apt sources

`echo 'deb http://urbit-on-arm.s3-website.us-east-2.amazonaws.com buster custom' | sudo tee /etc/apt/sources.list.d/urbit-on-arm.list`

#### Update the package list

`sudo apt update`

#### Install Urbit

`sudo apt install urbit`

↰ [Return to Index](index.md)
