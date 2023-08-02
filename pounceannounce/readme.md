# Description | 內容
Announces hunter pounces to the entire server

* Video | 影片展示
<br/>None

* Image | 圖示
	* Hunter high pounce
		> 顯示Hunter的高撲資訊
		<br/>![pounceannounce_1](image/pounceannounce_1.jpg)
	* Hunter high pounce instant kill
		> Hunter的高撲夠高造成致命一擊
		<br/>![pounceannounce_2](image/pounceannounce_2.jpg)

* Apply to | 適用於
	```
	L4D1
	L4D2
	```

* <details><summary>Changelog | 版本日誌</summary>

	* v1.9 (2023-3-24)
		* Remake code, convert code to latest syntax
		* Fix warnings when compiling on SourceMod 1.11.
		* Optimize code and improve performance
		* The minimum amount of damage required to instantly kill survivor.

	* v1.5
		* [Original Plugin by n0limit](https://forums.alliedmods.net/showthread.php?t=93605)
</details>

* Require | 必要安裝
	1. [[INC] Multi Colors](https://github.com/fbef0102/L4D1_2-Plugins/releases/tag/Multi-Colors)

* Related Plugin | 相關插件
	1. [l4d2_pounce_damage by Silvers](https://forums.alliedmods.net/showthread.php?p=2675236): Patches the Hunter to enable bonus damage in all gamemodes.
		> 任何模式的AI Hunter都可以造成高撲傷害
	2. [pounce_maxdamage](https://github.com/fbef0102/Rotoblin-AZMod/blob/master/SourceCode/scripting-az/pounce_maxdamage.sp): Makes it easy to properly uncap hunter pounces
		> (L4D1) 可以改變最大高撲的傷害值
	3. [accelerator74/Pounce-Damage-Uncap](https://github.com/accelerator74/Pounce-Damage-Uncap/actions): Change the pounce range and max pounce damage in L4D2
		> (L4D2) 可以改變最大高撲的傷害值

* <details><summary>ConVar | 指令</summary>

	* cfg/sourcemod/pounceannounce.cfg
		```php
        // Caps the displayed pounce damage to the maximum able to be dealt.
        pounceannounce_capdamage "0"

        // Announces the pounce to 0: chatbox, 1: center chat.
        pounceannounce_centerchat "0"

        // The minimum amount of damage required to instantly kill survivor. (0=Off)
        pounceannounce_killdamage "0"

        // The minimum amount of damage required to announce the pounce
        pounceannounce_minimum "10"

        // Show the distance the hunter traveled for the pounce.
        // 1=units, 2=units & feet, 3=units & meters, 4=feet, 5=meters
        pounceannounce_showdistance "3"
		```
</details>

* <details><summary>Command | 命令</summary>

	None
</details>

* <details><summary>How to change max pounce damage in l4d1</summary>

    1. Install [pounce_maxdamage](https://github.com/fbef0102/Rotoblin-AZMod/blob/master/SourceCode/scripting-az/pounce_maxdamage.sp)
	2. write down the following cvars in cfg/server.cfg
		```php
		// Sets the new maximum hunter pounce damage.
		sm_cvar pounceuncap_maxdamage 100
		```
</details>

* <details><summary>How to change max pounce damage in l4d2</summary>

    1. Install [accelerator74/Pounce-Damage-Uncap](https://github.com/accelerator74/Pounce-Damage-Uncap/actions)
	2. write down the following cvars in cfg/server.cfg
        * default 25
            ```php
            // z_pounce_damage_range_max = ((z_hunter_max_pounce_bonus_damage / 24) * 700) + z_pounce_damage_range_min
            sm_cvar z_hunter_max_pounce_bonus_damage 24
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 1000
            ```
        * Max Pounce Damage 30
            ```php
            // z_pounce_damage_range_max = ((29 / 24) * 700) + 300
            sm_cvar z_hunter_max_pounce_bonus_damage 29
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 1145.833
            ```
        * Max Pounce Damage 75
            ```php
            // z_pounce_damage_range_max = ((74 / 24) * 700) + 300
            sm_cvar z_hunter_max_pounce_bonus_damage 29
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 2458.333
            ```
        * Max Pounce Damage 100
            ```php
            // z_pounce_damage_range_max = ((99 / 24) * 700) + 300
            sm_cvar z_hunter_max_pounce_bonus_damage 99
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 3187.5
            ```
        * Max Pounce Damage 200
            ```php
            // z_pounce_damage_range_max = ((199 / 24) * 700) + 300
            sm_cvar z_hunter_max_pounce_bonus_damage 199
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 6104.167
            ```
</details>

- - - -
# 中文說明
顯示Hunter造成的高撲傷害與高撲距離

* 原理
	* 當AI Hunter或者真人Hunter造成高撲傷害時，顯示資訊給所有玩家
		* 受害者
        * 高撲傷害
        * 伺服器允許的最大高撲傷害
        * 距離
    * 當AI Hunter或者真人Hunter造成高撲傷害夠高時，造成倖存者當場死亡 (有指令可以關閉此功能)

* 功能
    * 可設置高撲傷害超過一個數值才會顯示
    * 可設置顯示在聊天室窗還是黑底白字提示窗
    * 可設置距離的顯示單位
    * 可設置高撲傷害超過一個數值會造成倖存者當場死亡或者關閉此功能

* <details><summary>惡靈勢力一代中修改最大高撲傷害</summary>

    1. 安裝 [pounce_maxdamage](https://github.com/fbef0102/Rotoblin-AZMod/blob/master/SourceCode/scripting-az/pounce_maxdamage.sp)
	2. 以下指令寫入文件 cfg/server.cfg，可自行調整
		```php
		// Sets the new maximum hunter pounce damage.
		sm_cvar pounceuncap_maxdamage 100
		```
</details>

* <details><summary>惡靈勢力二代中修改最大高撲傷害</summary>

    1. 安裝 [accelerator74/Pounce-Damage-Uncap](https://github.com/accelerator74/Pounce-Damage-Uncap/actions)
	2. 以下指令寫入文件 cfg/server.cfg，可自行調整
        * 預設最大高撲傷害: 25
            ```php
            // z_pounce_damage_range_max = ((z_hunter_max_pounce_bonus_damage / 24) * 700) + z_pounce_damage_range_min
            sm_cvar z_hunter_max_pounce_bonus_damage 24
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 1000
            ```
        * 最大高撲傷害: 30
            ```php
            // z_pounce_damage_range_max = ((29 / 24) * 700) + 300
            sm_cvar z_hunter_max_pounce_bonus_damage 29
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 1145.833
            ```
       * 最大高撲傷害: 75
            ```php
            // z_pounce_damage_range_max = ((74 / 24) * 700) + 300
            sm_cvar z_hunter_max_pounce_bonus_damage 29
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 2458.333
            ```
        * 最大高撲傷害: 100
            ```php
            // z_pounce_damage_range_max = ((99 / 24) * 700) + 300
            sm_cvar z_hunter_max_pounce_bonus_damage 99
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 3187.5
            ```
        * 最大高撲傷害: 200
            ```php
            // z_pounce_damage_range_max = ((199 / 24) * 700) + 300
            sm_cvar z_hunter_max_pounce_bonus_damage 199
            sm_cvar z_pounce_damage_range_min 300
            sm_cvar z_pounce_damage_range_max 6104.167
            ```
</details>

