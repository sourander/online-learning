# 1A: IaC Terraform

!!! tip

    Voit tehdä nämä Workshop-harjoitukset haluamaasi hakemistoon. Niiden ei tarvitse sijaita GitLab-reposiotiossa, johon varsinainen kurssityö on tarkoitus tehdä.

* Tee [IaC Terraform](https://gitlab.dclabra.fi/workshopit/iac-terraform)-workshop. 
* Kaikki vaiheet selitetään [Workshop: IaC Terraform](https://youtube.com/playlist?list=PL7AbISYtmmfiwaZSYNwIW-pDIOV17QNit)-YouTube-soittolistalla.

## Videoiden päävaiheet

Pääpiirteittäin vaiheet ovat:

1. Asenna ohjeiden mukaan omalle koneellesi Azure CLI ja Terraform CLI
2. Tee harjoitus "lesson_01 - Static Webpage".
    - Huom. Varmista, että saat nettisivun auki ja siellä on oikea sisältö!
3. Tee harjoitus "lesson_02 - Linux Virtual Machine".
    - Huom. Varmista, että saat SSH yhteyden koneeseen!
4. Muista tuhota kaikki resurssit kun lopetat työskentelyn!

!!! warning

    Jos jossakin vanhassa videossa viitataan siihen, että sinun tulee luoda **resource group**, kyseinen kohta vaatii refaktorointia! Uudessa Azure DevOps -ratkaisussa resurssiryhmä luodaan sinua varten automaattisesti, joten sinun tulee *viitata* siihen eikä yrittää luoda uutta. Sinulla ei ole oikeuksia luoda resurssiryhmiä. Alla on selvyyden vuoksi esitelty Terraform-koodi, jolla sellainen luodaan, ja koodi, jolla viitataan olemassa olevaan resurssiryhmään (data):

    ```hcl
    # Tämä koodi luo resurssiryhmän, mutta sinulla ei ole oikeuksia
    resource "azurerm_resource_group" "example" {
        name     = "${var.product}-rg-${var.suffix}"
        location = var.resource_group_location
    }
    ```

    ```hcl
    # Tämä luo viittauksen olemassa olevaan resurssiryhmään!
    data "azurerm_resource_group" "rg" {
        name = var.resource_group_name
    }
    ```

    Annetut koodiesimerkit ([gitlab:workshopit/iac-terraform](https://gitlab.dclabra.fi/workshopit/iac-terraform)) ovat päivitetty uuteen muotoon. Älä siis kopioida koodia videoista vaan käytä mallivastauksia ohjenuorana!