---
title: RainbowCalculator API
description: Generate the ideal mana base for a regular Magic the Gathering Commander deck.
date: 2022-08-13
---

Tha goal of this library is to calculate the mana source requirements (lands and mana generating artifacts) of a regular EDH/Commander deck in the trading card game Magic: the Gathering.

## API Setup

It's a simple API written in .NET 6 with only two endpoints, one of which is only used for testing purposes. This way any client can call the API and implement it the way they see fit. I chose to do it with a [Discord bot](https://discord.com/developers/docs/intro). See [this repository](https://github.com/LazarQt/RainbowFrog) on how it works and try it out yourself!

## API Call

*Request*

`POST: host:port/`

Parameters:

`Decklist` string array of the entire deck
`Ignorelands` string array of lands that should be ignored (in case user does not own this particular land)


Endpoint for making a simple get request and ensuring the server is running correctly:

*Request*

`GET /api/ping/`

    curl -i -H 'Accept: application/json' http://host:port/api/ping/

*Response*

    HTTP/1.1 200 OK
    Status: 200 OK
    Content-Type: application/json

    {
        id: 1,
        name: "Ping successful"
    }

Endpoint to request mana base suggestion:

*Request*

`POST /api/manabase/`

    curl -i -H 'Accept: application/json' -d 
    'decklist=["Card 1","Card 2"]&ignorelands=["Badlands"]' http://host:port/api/manabase/

*Response*

    HTTP/1.1 201 Created
    Status: 200 Created
    Connection: close
    Content-Type: application/json

    {
        "data": 
        {
            "error": null,
            "averageManaValue": "2.345",
            "relevantCardList": [
                "Card A",
                "Card B",
                "Card C"
            ],
            "cardsNotFound": [],
            "excludedCards": [
                "Card X",
                "Card Y",
                "Card Z"
            ],
            "removedLands": [
                "Land 1",
                "Land 2"
            ],
            "sources": [
                "1 Land A",
                "2 Land B"
            ],
            "sourcesCount": 2,
            "colorRequirementsErrors": [
                "Ignoring hybrid mana cost of this card",
            ],
            "colorRequirements": [
                {
                    "color": "b",
                    "amount": 33,
                    "amountFulfilled": 33,
                    "isFulfilled": true,
                    "cardResponsible": "Card Alpha"
                },
                {
                    "color": "g",
                    "amount": 29,
                    "amountFulfilled": 33,
                    "isFulfilled": true,
                    "cardResponsible": "Card Beta"
                }
            ],
            "manarockRatio": {
                "landsWithoutRocks": 38,
                "minMv": 2.08,
                "maxMv": 2.4,
                "manaRocks": 6,
                "lands": 35
            }
        }
    }


*Response contents*

Property | Message 
--- | --- 
error | If calculation throws an error, this is where it is shown 
averageManaValue | Average mana value of deck
relevantCardList | All the cards that are "relevant" to the calculation (some cards are excluded, based on methodology)	
cardsNotFound | Cards that are not found (typo?)
excludedCards | Cards taht are excluded because they are not required for calculation
removedLands | Lands that were removed prior to calculation in case user forgot to take them out
sources | Suggested sources
sourcesCount | How many sources there are
colorRequirementsErrors | If a card is NOT taken into account when it comes to calculations, this is where it is shown why	
colorRequirements | Color requirements for each color
manarockRatio | How many lands and mana rocks are needed

## Methodology

The full readme including the methodology how the calculations are made can be found [here](https://github.com/LazarQt/RainbowCalculator) on the GitHub project repository.
