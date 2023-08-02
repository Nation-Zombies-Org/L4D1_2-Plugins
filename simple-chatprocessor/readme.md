# Description | 內容
Process chat and allows other plugins to manipulate chat.

* Video | 影片展示
<br/>None

* Image | 圖示
<br/>None

* Apply to | 適用於
	```
	L4D1
	L4D2
	```

* <details><summary>Changelog | 版本日誌</summary>

	* v1.3h (2023-7-5)
		* Fixed Crash

	* v1.2h (2023-6-16)
		* Fixed error "Exception reported: Unable to end message, no message is in progress"

	* v1.1h (2023-6-15)
		* L4D1/2 Only
		* Add chinese translation 

	* v1.0h (2023-3-12)
		* Delete API OnChatMessage(int &author, ArrayList recipients, char[] name, char[] message)
        * Add API OnChatMessage2(int &author, ArrayList recipients, char[] name, int maxlength_name, char[] message, int maxlength_message)
        * Fixed translation file error in l4d1/l4d2

	* v2.3.0
		* [JoinedSenses's fork](https://github.com/JoinedSenses/SM-Custom-ChatColors-Menu)

	* 2.0.2
		* [Original Plugin by minimoney1](https://forums.alliedmods.net/showthread.php?t=198501)
</details>

* Require | 必要安裝
<br/>None

* Related Plugin | 相關插件
	1. [sm_regexfilter](https://github.com/fbef0102/Game-Private_Plugin/tree/main/Plugin_%E6%8F%92%E4%BB%B6/Anti_Griefer_%E9%98%B2%E6%83%A1%E6%84%8F%E8%B7%AF%E4%BA%BA/sm_regexfilter): Filter dirty words via Regular Expressions
		> 禁詞表，任何人打字說出髒話或敏感詞彙，字詞會被屏蔽、玩家禁言並處死，網路並非法外之地
	2. [l4d_mute_player_list](https://github.com/fbef0102/Game-Private_Plugin/tree/main/Plugin_%E6%8F%92%E4%BB%B6/Anti_Griefer_%E9%98%B2%E6%83%A1%E6%84%8F%E8%B7%AF%E4%BA%BA/l4d_mute_player_list): Player can personally mute someone chat text and mic voice.
		> 玩家可以在個人列表上封鎖其他人的語音與聊天文字
	3. [simple-chatcolors](https://github.com/fbef0102/Game-Private_Plugin/tree/main/Plugin_%E6%8F%92%E4%BB%B6/Fun_%E5%A8%9B%E6%A8%82/simple-chatcolors): Changes the colors of players chat based on config file.
		> 根據管理員或玩家身分修改聊天窗口的對話顏色

* <details><summary>ConVar | 指令</summary>

	None
</details>

* <details><summary>Command | 命令</summary>

	None
</details>

* <details><summary>API | 串接</summary>

	```c++
	/**********************************************************************
	* Gets the current flags for the chat message
	* Should only be called within OnChatMessage2() or OnChatMessage_Post()
	*
	* @return		The current type of chat message (see constants) 
	**********************************************************************/
	native int GetMessageFlags();

	/**********************************************************************
	* When a player types a chat message
	*
	* NOTES:
	* Use MAXLENGTH_  constants above for formating the strings
	* Do not rely on the recipients handle to exist beyond the forward
	* Do not start another usermessage (PrintToChat) within this forward
	*
	* @param 		author						The client index of the player who sent the chat message (Byref)
	* @param 		recipients					The handle to the client index adt array of the players who should recieve the chat message
	* @param 		name						The client's name of the player who sent the chat message (Byref)
	* @param 		maxlength_name				Maximum length of name string to store to
	* @param 		message						The contents of the chat message (after any replacements)
	* @param 		maxlength_message			Maximum length of message string to store to
	* @return									Plugin_Stop to block chat message, Plugin_Changed to use overwritten values from plugin, Plugin_Continue otherwise
	**********************************************************************/
	forward Action OnChatMessage2(int &author, ArrayList recipients, char[] name, int maxlength_name, char[] message, int maxlength_message);

	/**********************************************************************
	* Called after all OnChatMessage2 forwards have been fired and the message is being broadcast.
	*
	* NOTES:
	* Use MAXLENGTH_  constants above for formating the strings
	* Do not rely on the recipients handle to exist beyond the forward
	*
	* @param 		author						The client index of the player who sent the chat message
	* @param 		recipients					The handle to the client index adt array of the players who are receiting the chat message
	* @param 		name						The client's name of the player who sent the chat message (after any replacements)
	* @param 		message						The contents of the chat message (after any replacements)
	* @noreturn
	**********************************************************************/
	forward void OnChatMessage_Post(int author, ArrayList recipients, const char[] name, const char[] message);
	```
</details>

- - - -
# 中文說明
輔助插件，控制玩家在聊天窗口輸入的文字與顏色

* 原理
	* 這插件只是一個輔助插件，能夠攔截玩家在聊天窗口輸入的文字
	* 等其他插件需要的時候再安裝

* 功能
	* 改變聊天中的名子、文字、顏色、接收對象

