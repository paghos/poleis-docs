Minerva uses any external OAuth provider for user management.
Our environment (and the only one tested) is built using [Keycloak](https://keycloak.org).

Dear Italian users, with Keycloak you can integrate the SPID authentication, thanks to [developers.italia.it](https://github.com/italia) efforts. More info can be found [here](https://github.com/italia/spid-keycloak-provider).

## 1. Configure Minerva (or any Poleis software) to work with Keycloak 

We realized this guide that helps you to create the OAuth client using Keycloak admin portal.

<iframe src="https://scribehow.com/embed/Configurare_Keycloak_come_Identity_Provider_della_Poleis_suite___02lA942Sr65oiUXtkgoOA" width="100%" height="640" allowfullscreen frameborder="0"></iframe>

After completing the steps of this guide, keep following the Environment Configuration guide for your app. Minerva one can be found [here.](/Minerva/Environment%20configuration/#1-filling-the-appconf-section) Chronos one can be found [here.](/Chronos/Environment setup/#1-filling-the-appconf-section)

## Disclaimer

Other identity providers may be supported, as OAuth is an open standard, they aren't just tested.

You found another IAM software compatible with the Poleis suite? Send us an [email](mailto:hello@poleis.cloud)

