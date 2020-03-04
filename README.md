[![Build Status](https://travis-ci.org/blockchain-certificates/cert-tools.svg?branch=master)](https://travis-ci.org/blockchain-certificates/cert-tools)

# cert-tools
Command line tools for designing certificate templates, instantiating a certificate batch, and import/export tasks

see example of certificate template and batch creation in sample_data 

## Install

1. Ensure you have an python environment. [Recommendations](https://github.com/blockchain-certificates/cert-issuer/blob/master/docs/virtualenv.md)

2. Git clone the repository and change to the directory

  ```bash
  git clone https://github.com/vinnayb29/cert-tools.git && cd cert-tools
  ```

3. Run the setup script

  ```bash
  pip install .
  ```
4. Go to sample_data/roasters in cert-tools folder and edit the roster_testnet.csv
 
## Scripts

The cert-tools setup script installs 2 scripts, which are described below:


### create_certificate_template.py

#### Run

```bash
create-certificate-template -c conf.ini
```

#### Configuration

The `conf.ini` fields are described below. Optional arguments are in brackets

```
create-certificate-template --help

usage: create_v2_certificate_template.py [-h] [-c MY_CONFIG]
                                         [--data_dir DATA_DIR]
                                         [--issuer_logo_file ISSUER_LOGO_FILE]
                                         [--cert_image_file CERT_IMAGE_FILE]
                                         [--issuer_url ISSUER_URL]
                                         [--issuer_certs_url ISSUER_CERTS_URL]
                                         --issuer_email ISSUER_EMAIL
                                         --issuer_name ISSUER_NAME
                                         --issuer_id ISSUER_ID [--issuer_key ISSUER_KEY]
                                         [--certificate_description CERTIFICATE_DESCRIPTION]
                                         --certificate_title CERTIFICATE_TITLE
                                         --criteria_narrative CRITERIA_NARRATIVE
                                         [--template_dir TEMPLATE_DIR]
                                         [--template_file_name TEMPLATE_FILE_NAME]
                                         [--hash_emails]
                                         [--revocation_list REVOCATION_LIST]
                                         [--issuer_public_key ISSUER_PUBLIC_KEY]
                                         --badge_id BADGE_ID
                                         [--issuer_signature_lines ISSUER_SIGNATURE_LINES]
                                         [--additional_global_fields ADDITIONAL_GLOBAL_FIELDS]
                                         [--additional_per_recipient_fields ADDITIONAL_PER_RECIPIENT_FIELDS]


Args that start with '--' (eg. --data_dir) can also be set in a config file (./cert-tools/conf.ini or specified via -c). Config file syntax allows: key=value, flag=true, stuff=[a,b,c] (for details, see syntax at https://goo.gl/R74nmi). If an arg is specified in more than one place, then commandline values override config file values which override defaults.


Argument details:
  -h, --help            show this help message and exit
  -c MY_CONFIG, --my-config MY_CONFIG
                        config file path (default: None)
  --data_dir DATA_DIR   where data files are located (default: None)
  --issuer_logo_file ISSUER_LOGO_FILE
                        issuer logo image file, png format (default: None)
  --cert_image_file CERT_IMAGE_FILE
                        issuer logo image file, png format (default: None)
  --issuer_url ISSUER_URL
                        issuer URL (default: None)
  --issuer_certs_url ISSUER_CERTS_URL
                        issuer certificates URL (default: None)
  --issuer_email ISSUER_EMAIL
                        issuer email (default: None)
  --issuer_name ISSUER_NAME
                        issuer name (default: None)
  --issuer_id ISSUER_ID
                        issuer profile (default: None)
  --issuer_key ISSUER_KEY
                        issuer issuing key (default: None)
  --certificate_description CERTIFICATE_DESCRIPTION
                        the display description of the certificate (default:
                        None)
  --certificate_title CERTIFICATE_TITLE
                        the title of the certificate (default: None)
  --criteria_narrative CRITERIA_NARRATIVE
                        criteria narrative (default: None)
  --template_dir TEMPLATE_DIR
                        the template output directory (default: None)
  --template_file_name TEMPLATE_FILE_NAME
                        the template file name (default: None)
  --hash_emails         whether to hash emails in the certificate (default:
                        False)
  --revocation_list REVOCATION_LIST
                        issuer revocation list (default: None)
  --issuer_public_key ISSUER_PUBLIC_KEY
                        issuer public key (default: None)
  --badge_id BADGE_ID   badge id (default: None)
  --issuer_signature_lines ISSUER_SIGNATURE_LINES
                        issuer signature lines (default: None)
  --additional_global_fields ADDITIONAL_GLOBAL_FIELDS
                        additional global fields (default: None)
  --additional_per_recipient_fields ADDITIONAL_PER_RECIPIENT_FIELDS
                        additional per-recipient fields (default: None)


```

#### About

Creates a certificate template populated with the setting you provide in the conf.ini file. This will not contain recipient-specific data; such fields will be populated with merge tags.
 

### instantiate_certificate_batch.py

#### Run

```
instantiate-certificate-batch -c conf.ini
```


#### About

Populates the certificate template (created by the previous script) with recipient data from a csv file. It generates a certificate per recipient based on the values in the csv file.

The csv file location is configurable via the conf.ini file.

The csv file must always contain:

- name
- pubkey
- identity

#### Configuration

The `conf.ini` fields are described below. Optional arguments are in brackets


```
instantiate-certificate-batch --help

usage: instantiate_v2_certificate_batch.py [-h] [-c MY_CONFIG]
                                           [--data_dir DATA_DIR]
                                           [--issuer_certs_url ISSUER_CERTS_URL]
                                           [--template_dir TEMPLATE_DIR]
                                           [--template_file_name TEMPLATE_FILE_NAME]
                                           [--hash_emails]
                                           [--additional_per_recipient_fields ADDITIONAL_PER_RECIPIENT_FIELDS]
                                           [--unsigned_certificates_dir UNSIGNED_CERTIFICATES_DIR]
                                           [--roster ROSTER]

Args that start with '--' (eg. --data_dir) can also be set in a config file (./cert-tools/conf.ini or specified via -c). Config file syntax allows: key=value, flag=true, stuff=[a,b,c] (for details, see syntax at https://goo.gl/R74nmi). If an arg is specified in more than one place, then commandline values override config file values which override defaults.

Argument details:
  -h, --help            show this help message and exit
  -c MY_CONFIG, --my-config MY_CONFIG
                        config file path (default: None)
  --data_dir DATA_DIR   where data files are located (default: None)
  --issuer_certs_url ISSUER_CERTS_URL
                        issuer certificates URL (default: None)
  --template_dir TEMPLATE_DIR
                        the template output directory (default: None)
  --template_file_name TEMPLATE_FILE_NAME
                        the template file name (default: None)
  --hash_emails         whether to hash emails in the certificate (default:
                        False)
  --additional_per_recipient_fields ADDITIONAL_PER_RECIPIENT_FIELDS
                        additional per-recipient fields (default: None)
  --unsigned_certificates_dir UNSIGNED_CERTIFICATES_DIR
                        output directory for unsigned certificates (default:
                        None)
  --roster ROSTER       roster file name (default: None)

```


## Contact

Contact us at [the Blockcerts community forum](http://community.blockcerts.org/).
