# AnsiblePackerAuto

## About

AnsiblePackerAuto is a simple program that uses [`Packer`](https://www.packer.io/) for building an image for my CP while using [`Ansible`](https://www.ansible.com/) to provision the image.

### Instructions
The following instructions shouw the steps taken to build the image

1. Clone the repository and `cd` into `AnsiblePackerAuto` directory

    ```
     git clone https://github.com/Davitron/AnsiblePackerAuto.git
     
     cd AnsiblePackerAuto
    ```
2. open the `packer_ec2.json` file in a text editor. The script is divided into 3 sections which are the `variables`, `builders` and the `provisioners`
3. specify the AWS security credentials as specified in the script

	```
	"variables": {
      "aws_access_key": "{{env `AWS_ACCESS_KEY_ID`}}",
      "aws_secret_key": "{{env `AWS_SECRET_ACCESS_KEY`}}"
    },
    ```
    To maintain the security and integrity of this script, iOt is adviced that both credentials are exported as global env vatiables
    
    ```
    $ export AWS_ACCESS_KEY_ID=hgroehgoruwhgrouwhgroueghoeg
    $ export AWS_SECRET_ACCESS_KEY=30t843u0g8hrwg2nighrw0gh2giw8ruy20
    ```
4. In the playbook_main.yml, specify the following environment variables as specified in the file

	```
	 - name: set env
      shell:
        cmd: |
          cat > /home/ubuntu/EventsManagerApp/.env <<EOF
          DATABASE_URL=<POSTGRESQL DATABASE URL>
          SECRET_KEY=<JWT SECRET>
          EMAIL_ADDRESS=<MAILING SERVICE EMAIL ADDRESS>
          EMAIL_PASSWORD=<MAILING SERVICE PASSWORD>
          EOF
   ```
5. Build the image, by running

   ```
   packer build packer_ec2.json
   ```
    


