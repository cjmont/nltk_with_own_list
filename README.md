# MNLOPDPartnerMyBusiness

### The code allows us to use our own list of first and last names in conjunction with nltk

This Python module is designed to work with Odoo and provides functionality to interact with Odoo's partner model (`res.partner`). This code is part of an Odoo module and needs to be within a valid module directory structure to work properly.

The code is divided into several sections. It loads a list of names and surnames, defines a new class `MNLOPDPartnerMyBusiness` that inherits from `res.partner`, and then defines various methods within this class to perform certain functions.

## Features

* Loading names and surnames from text files.
* Splitting the full name into first name and last name.
* Sending data to an API when certain fields are modified in the `res.partner` model.
* Retrying the request to the API if it fails.
* Logging the API's response or error in the model's fields.

## Requirements

For this code to work, you need:

* Python 3.6+
* Odoo 14.0+
* The Python libraries `requests`, `nltk`, and `configparser`.
* The `ec_nombres.txt` and `ec_apellidos.txt` files in the module's data directory.

## Installation

This module should be installed into an Odoo instance. Here are the basic steps to install a module in Odoo:

1. Copy the module folder into your Odoo installation's module folder.
2. Update the module list in Odoo (Update Application List).
3. Install the module through Odoo's user interface.

## Usage

This module activates automatically when a record in Odoo's `res.partner` model is created or modified.

## Support

This is an open-source module. For issues and enhancements, you can open an issue in the module's repository.

## Contributing

To contribute to this project, fork the repository, make your changes, and then submit a pull request.

## License

This project is licensed under the AGPL-3 license.

## Warning

This code disables SSL verification when making requests to the API. This may expose the system to certain security risks. Use it with caution.

## Additional Comment

This code is written in Python and uses the Odoo ORM (Object-Relational Mapping) framework to define a new Model. This new Model extends the `res.partner` model which represents partners, companies, customers, etc., in Odoo.

This model introduces two new fields to store status code and logs: `mb_status_code_log` and `mb_text_log`.

It also adds a method to split a given full name into first name and last name. The splitting logic checks if the part of a name exists in a known list of first names from nltk (Natural Language Toolkit) corpus. If it does, it considers it as a first name, else a last name.

There are several methods overridden from the base model:

- `_onchange_mnlopdp_otp`: This method is triggered when `mnlopdp_otp` field value changes. It sends some data using a POST request when this happens.
- `create`: This method is overridden to send data using a POST request after a new partner is created.
- `write`: This method is overridden to send data using a PUT request when specific fields are updated.

Finally, the `_send_data` method is defined to send data to a specified API endpoint using either POST or PUT methods depending on the input. It sends a bunch of partner data like name, email, mobile, etc. It handles exceptions and retries failed requests up to 2 times with a delay of 3 seconds between each retry.

