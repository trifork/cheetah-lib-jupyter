# jupyterAuth

A plugin module for authenticate in different scopes using Python Jupyter Notebook as base and a given IDP.

## Project structure

The project is structured as follows:
- `/jupyterAuth` - Contains all source code.
- `/tests` - Contains all unit tests (unittest).
- `requirements.txt` - This file contains all the modules required for the application.
- `pyproject.toml` - This file contains the instructions for build the module when will be imported from `pip`
- `README.md` - This file, contains internal developer documentation.

## Prerequisites
- Python >= 3.10
- [cheetah-development-infrastructure](https://github.com/trifork/cheetah-development-infrastructure) is cloned and running.

## Parameters 

All parameters for create an `Authorizer` object are:

- Instantiation argument: **<service host>** , **<prometheus port>**, **<oauth address endpoint>** , **<scope>** , **<disable https>**
  - **service host**: The address of the service that you want to authenticate (leave "" if not `"opensearch"`)
  - **prometheus port**: The port of prometheus service (leave "", is not developed yet)
  - **oauth address endpoint**: The address of the IDP endopoint that provide the authentication
  - **scope**: The service that you want to authenticate e.g. `"kafka"`, `"opensearch"`
  - **disable https**: If `True` authentication credentials will be transferred by HTTP

All parameters for use an `Authorizer` with `getJWToken` and `getOauth2` are:

- Instantiation argument: **<username>** , **<password>**
  - **username**
  - **password**

### Examples

To create an `Authorizer` object pre-setted within Kafka in local environment (using HTTP) without using Prometheus:

```python
authorizer_object = Authorizer("", "" , "http://localhost:1852/realms/local-development/protocol/openid-connect/token", "kafka", True)
```

To use the `Authorizer` for get a JWToken given the credentials

```python
token = authorizer_object.getJWToken("username", "password")
```

### Warn

- Can work in local environment with HTTP and so the authentication credentials will be transferred in plaintext.
