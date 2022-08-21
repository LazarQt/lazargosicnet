---
title: DraftHelperSync
description: Synchronize data between [17lands](https://www.17lands.com/) and [MTGAHelper](https://mtgahelper.com/).
date: 2021-10-06
---

[MTGAHelper](https://mtgahelper.com/) is a tool that can be used to make notes for specific cards while playing Magic the Gathering Arena.

Meanwhile there exist a site called [17lands](https://www.17lands.com/) which analyzes user logs to gather information about card performance in Magic the Gathering Arena.

The tool I wrote draws the logical conclusion and updates the card notes with data from 17lands API. (In addition to some calculations to display the power level of an individual card appropriately)

<picture>
  <img alt="a very cute cat" src="/assets/img/drafthelpersync.png" />
</picture>

It's very simple and very effective. After the initial configuration the tool can run without the need for manual updates, all the required information is being pulled from the sites APIs where the synchronization happens.