'cm' for creative mode

'giveselfxp 10000'

'killall'

'help'

giveself itemName [qualityLevel=6] [count=1] [putInINventory=false] [spawnWithMods=true]
]]

# Noise

Probably add this to an 'effect_group' for an item:

		<passive_effect name="NoiseMultiplier" operation="perc_add" value=".1"/><display_value name="dNoiseMultiplier" value=".1"/>


# Cool mods:

  modGunMeleeRadRemover - 

```xml
<effect_group tiered="false">
  <requirement name="EntityTagCompare" target="other" tags="radiated"/>
  <triggered_effect trigger="onSelfDamagedOther" action="AddBuff" target="other" buff="buffRadiatedRegenBlock"/>
</effect_group>
```

modGunMeleeBlessedMetal

```xml
<effect_group tiered="false">
  <requirement name="EntityTagCompare" target="other" tags="zombie"/>
  <passive_effect name="EntityDamage" operation="perc_add" value="1"/>
</effect_group>
```

# admin items

possibly the reason they don't appear is because this is here:

  <property name="CreativeMode" value="Dev"/>





# Info

Intertesting, mods seem to give bonuses, i.e. stone axe gets 10% EntityDamage,BlockDamage for each mod?

## Harvesting

* meleeToolRepairT0StoneAxe - Has 'HarvestCount' with tags 'butcherHarvest', value 0.7
  * Has negative damage (earth -85%, stone -33%, metal -50%) as perc_add damage modifiers
  * AttcksPerMinute

Things to look at:

Chainsaw Action0 has 'SupportHarvesting' true, 'ToolCategory.harvestingTools' value 1 param1 1

meleeToolSalvageT1Wrench has Actino0:

		<property name="ToolCategory.harvestingTools" value=".5" param1="1"/>
		<property name="ToolCategory.Disassemble" value="1" param1="1"/>
		<property name="Particle_harvesting" value="true" param1="metal"/>

And effect group:

	  <passive_effect name="HarvestCount" operation="base_set" value="1" tags="salvageHarvest"/>
	
Axes have ".7" value 'butcherHarvest'

Wooden club has THREE:

		<passive_effect name="HarvestCount" operation="base_add" value="-.75" tags="allHarvest"/>
		<passive_effect name="HarvestCount" operation="base_add" value="-.75" tags="allToolsHarvest"/>
		<passive_effect name="HarvestCount" operation="base_add" value="-.75" tags="oreWoodHarvest"/>

Baton has 4:

		<passive_effect name="HarvestCount" operation="base_set" value="1" tags="butcherHarvest"/>

		<passive_effect name="HarvestCount" operation="base_add" value="-.75" tags="allHarvest"/>
		<passive_effect name="HarvestCount" operation="base_add" value="-.75" tags="allToolsHarvest"/>
		<passive_effect name="HarvestCount" operation="base_add" value="-.75" tags="oreWoodHarvest"/>

Steel knuckles have:

		<passive_effect name="HarvestCount" operation="base_set" value="1" tags="butcherHarvest"/>

meleeToolSalvageWrenchAdmin has:

		<passive_effect name="HarvestCount" operation="base_set" value="1" tags="salvageHarvest"/>

meleeToolHammerOfGodAdmin has:

  Action 0:

    <property name="ToolCategory.Butcher" value="0" param1="4"/>
    <property name="ToolCategory.harvestingTools" value="1" param1="1"/>

		<passive_effect name="HarvestCount" operation="base_set" value="1" tags="butcherHarvest"/>

Interesting effect groups on equip:

		<triggered_effect trigger="onSelfEquipStart" action="AddBuff" buff="buffDontBreakMyLeg"/>
		<triggered_effect trigger="onSelfEquipStop" action="RemoveBuff" buff="buffDontBreakMyLeg"/>

And coolLootShadesAdmin

		<passive_effect name="LootGamestage" operation="base_add" value="100"/>
		<passive_effect name="TreasureRadius" operation="base_add" value="-5"/>
		<display_value name="dTreasureRadius" value="-5"/>


And 'toubhGuyShirtAdmin':

		<passive_effect name="HypothermalResist" operation="base_add" value="1.8,4.2"/>
		<passive_effect name="HyperthermalResist" operation="base_add" value="7.5,10.5"/>
		<passive_effect name="HealthMax" operation="base_add" value="19900"/><display_value name="dHealthMax" value="20000"/>
		<passive_effect name="HealthMax" operation="base_subtract" value="@$PlayerLevelBonus"/>

'pimpMiningHelmetAdmin' is neat:

		<passive_effect name="HypothermalResist" operation="base_add" value="100"/>
		<passive_effect name="HyperthermalResist" operation="base_add" value="100"/>

		<passive_effect name="DegradationMax" operation="base_set" value="9999" tags="admin"/>
		<passive_effect name="DegradationPerUse" operation="base_set" value="0" tags="admin"/>

'armorPlotAdmin':

		<passive_effect name="PhysicalDamageResist" operation="base_add" value="81.25"/>
		<passive_effect name="ElementalDamageResist" operation="base_add" value="81.25" tags="heat,electrical"/>
		<passive_effect name="DegradationMax" operation="base_set" value="9999" tags="admin"/>
		<passive_effect name="DegradationPerUse" operation="base_set" value="0" tags="admin"/>
		<passive_effect name="BuffResistance" operation="base_add" value=".343" tags="buffFatiguedTrigger,buffArmSprainedCHTrigger,buffLegSprainedCHTrigger,buffInjuryBleedingTwo,buffInjuryBleedingBarbedWire,buffLaceration,buffInfectionCatch,buffInjuryStunned01CHTrigger"/>


## Super Stone Axe

```xml
<items>
  <item name="meleeToolRepairT0StoneAxe">
  	<property class="Action0">
  		<property name="ToolCategory.Butcher" value="0" param1="4"/><!-- damage vs entity corpses -->
  	<property class="Action1"> <!-- UseAction -->
      <property name="Class" value="Repair"/>
      <property name="Delay" value=".64"/> <!-- Repair actions still need the delay amount -->
      <property name="Repair_amount" value="100"/>
      <property name="Upgrade_hit_offset" value="-1"/>
      <property name="Sound_start" value="repair_block"/>
      <property name="Allowed_upgrade_items" value="resourceWood,resourceClayLump,resourceSnowBall,resourceScrapIron,resourceForgedIron,resourceForgedSteel,resourceConcreteMix,resourceCobblestones,ironDoor1_v1,vaultDoor01,scrapHatch_v1,vaultHatch_v1,resourceYuccaFibers,resourceCloth,resourceScrapPolymers"/>
      <property name="UsePowerAttackAnimation" value="false"/>
    </property>
    <effect_group name="meleeToolRepairT0StoneAxe">
      <passive_effect name="EntityDamage" operation="base_set" value="6" tags="perkMiner69r"/>
      <passive_effect name="BlockDamage" operation="base_set" value="21.5" tags="perkMiner69r"/>
      <passive_effect name="AttacksPerMinute" operation="base_set" value="105" tags="perkMiner69r,axe"/>
      <passive_effect name="StaminaLoss" operation="base_set" value="8" tags="primary"/>
      <passive_effect name="DegradationMax" operation="base_set" value="112,300" tier="1,6" tags="perkMiner69r"/>
      <passive_effect name="DegradationPerUse" operation="base_set" value="1" tags="perkMiner69r"/>
      <display_value name="dBlockRepairAmount" value="100"/>
      <passive_effect name="HarvestCount" operation="base_set" value=".7" tags="butcherHarvest"/>
      <passive_effect name="DamageModifier" operation="perc_add" value="-.85" tags="earth"/>
      <passive_effect name="DamageModifier" operation="perc_add" value="-.33" tags="stone"/>
      <passive_effect name="DamageModifier" operation="perc_add" value="-.5" tags="metal"/>
      <passive_effect name="DamageModifier" operation="base_set" value="1" tags="head,perkMiner69r" match_all_tags="true"/>
      <passive_effect name="DismemberChance" operation="base_set" value=".05"  tags="perkMiner69r"/>
  	</effect_group>
```

# Looting

* buffDrugEyeKandy - LootGamestage +5, +10%
  * Item drugEyeKandy
    * ModifyCVar - $buffDrugEyeKandyDuration add 303, max 903
    * AddBuff buffDrugEyeKandy
* apparelAviatorGoggles - LootGameStage (3-5.2), also TreasureBlocksPerReduction base_add=-1

## So what does LootGameStage do?

Say you have Aviator Goggles with high +5 LootGameStage.  And you use Eye Kandy which gies flat +5 PLUS 10%.
If your GameStage is 82, that would bump it to 92 + 9.2 = 101.2

* baseProbTemplate - 1-100 gives you 0.25 chance, 101-200 gives 0.5 chance.  So at 82, combo would give you twice the chance of getting the loot

