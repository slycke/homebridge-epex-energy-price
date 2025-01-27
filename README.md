# EPEX day ahead electricity price in Homebridge

This plugin will get energy prices (electricity) in Europe via the EPEX day ahead spot price (https://www.epexspot.com/en) published via the public ENTSO-E transparency platform (https://transparency.entsoe.eu).

The plugin will publish the EPEX Energy Price data (updated hourly) as a "temperature" sensor. The idea is that it can subsequently be used in HomeKit Automations to control other acessories.

If no EPEX Energy Price can be retrieved a default value (100, configureable) will be published.

# EPEX Electricity price data access and this plugin

> [!IMPORTANT]
> This Homebridge plugin requires that you obtain your own API security token on ENTSO-E in order to access the data. It is free (as in free beer) and easy enough but takes some time to do.
>
>Instructions here: (https://transparencyplatform.zendesk.com/hc/en-us/articles/12845911031188-How-to-get-security-token)

---

## Installation

The easiest installation method is to use Homebridge Configuration UI and search for this plugin.

## EPEX Day-ahead energy price data

The ENTSO-E API returns energy price data in the units EUR/MWh without any local taxes (e.g. VAT etc.). Because this plugin is mainly for domestic use the energy price is converted to EUR/kWh.

In the Netherlands in 2025 you pay the following additional costs (which are in fact much higher than the actual energy price):
* Purchasing fee for the Utility company: typically 2 ct/kWh
* National Energy Tax: 6.9 ct/kWh (2025)
* VAT: 21% on the alreay taxed amount.

So, if EPEX is 0.0 ct/kWh (so free energy) you still pay (6.9 + 2) * 1.21 = 10.7 ct/kWh.

Because EPEX can become negative it is interesting to know when the net, actual, price you pay the utility is also negative. In the Netherlands (2025) this happens at EPEX prices lower than -9 ct/kWh. At that point dynamic pricing energy is actually really free for the end consumer (while you still pay taxes...).

## Configuration

### Country - EIC Bidding Zone
You need to configure the region/country from which you want to get the EPEX Energy Price data. This is called the Bidding Zone EIC information and you can get the codes you need here: (https://transparencyplatform.zendesk.com/hc/en-us/articles/15885757676308-Area-List-with-Energy-Identification-Code-EIC)

For example for the Netherlands, use: `BZN|NL`

### Country - EIC Bidding Zone

You need to obtain your own API security token on ENTSO-E in order to access the data. It is free (as in free beer) and easy enough but takes some time to do.

Instructions [here](https://transparencyplatform.zendesk.com/hc/en-us/articles/12845911031188-How-to-get-security-token).

### Configuration Summary

| **Option**       | **Title**                                | **Type**   | **Required** | **Default**                  | **Description**                                                                                     |
|------------------|------------------------------------------|------------|--------------|------------------------------|-----------------------------------------------------------------------------------------------------|
| `name`           | Name                                     | string     | Yes          | EPEX Energy Price Monitor    | The name of your accessory as it will appear in Homebridge/HomeKit.                                 |
| `refreshInterval`| Refresh Interval (minutes)               | integer    | No           | 15                           | How often (in minutes) to poll ENTSO-E for updated price data. The minimum recommended is **15**.   |
| `in_Domain`      | Country / In-Domain (Bidding Zone)       | string     | Yes           | 10YNL----------L             | The ENTSO-E Bidding Zone Code representing the receiving energy area.                               |
| `apiKey`         | ENTSO-E API Key                          | string     | Yes           | *(empty)*                    | If your ENTSO-E account requires an API key, enter it here.                                         |
| `max_price`      | Maximum Price                            | integer    | No           | 100                          | Fallback for the maximum energy price if data is missing. Cannot exceed **100**.                    |
