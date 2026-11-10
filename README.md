# fenix-FXSound

《王者世界》（Atlantica Online）Fenix 凤凰服的配音仓库：用来在机器之间传输配音文件，并记录配音的制作过程、成品清单和待办事项。

游戏里的语音目录是 `FXSound`，分三大类：

- `BUDDY`：佣兵语音，按角色一个文件夹
- `NPC`：NPC 语音，按 `NPC\类别\NPC名` 分文件夹
- `MAIN`：主角语音
- 根目录另有 `FXSoundInfo.ndt` / `FXSoundInfo.vkr` 两个索引文件，只有英文客户端里有

音频格式统一为 `.ogg`。注意文件名后缀大多写着 `_KOR`，但里面实际装的语言中英日韩都有，后缀完全指望不上，判断语言只能靠听或转写。

## 素材现状（2026-11-10）

| 素材 | 条数 | 说明 |
| --- | --- | --- |
| eng（英文客户端提取） | 1709 条 ogg | BUDDY 105 个角色夹 / 1048 条，另有 NPC、MAIN |
| cn（中文残集） | 687 条 ogg | NPC 482 + BUDDY 190（43 个角色夹）+ MAIN 15；以 NPC 台词为主，不是全量 |
| 当年中文备份全量 | 2106 条 | 本地已删除，未恢复；且经抽查是中英日韩混装，并非纯中文 |

cn 的 43 个 BUDDY 角色夹全部是 eng 105 个角色夹的子集；cn 和 eng 互有缺失，没有包含关系。

## 已完成成品

两个成品包都已上传到 cstcloud 的 `hxsn/fenix/` 目录（预签名直链实测不可用、会返回 401，取包走 cstcloud 自己的入口）：

### 1. ETERNITY 配音整批（2026-11-07 跑完）

- 范围：eng 有、cn 没有的 BUDDY 台词，共 **873 条 / 101 个角色**，全量配中文，不筛选
- 结果：729 条自动质检通过，144 条被标出（自动质检没过、保留了最好的一版，等人工听审定留 / 重配 / 去掉）
- 成品包：`eternity_dub_batch_20261107.zip`，13,205,627 字节，873 个 ogg，md5 `03a31608492a2fffaf8fecaf8b624b6b`

### 2. cn_on_fenix 合并包（2026-11-08）

把 cn 和 eng 按文件夹合并成一份能直接给凤凰服用的 FXSound：

- 规则：**文件夹级合并**——某个文件夹 cn 里有就整夹用 cn 的，没有就用 eng 的；BUDDY、NPC、MAIN 三层都套这个规则，NPC 以 `NPC\类别\NPC名` 为一个单位；根目录的 FXSoundInfo 用 eng 的
- 配音成品不并入这个包
- 成品包：`cn_on_fenix.zip`，84,076,021 字节，顶层是 `FXSound/`，共 1554 个文件（1552 条 ogg：BUDDY 864 + NPC 617 + MAIN 71，另加 2 个 FXSoundInfo），md5 `54f8e95bc74471a58ca2c70a8451748f`

## 配音制作约定

- 本地管线全量跑，语速 **0.8**
- 音量：成品统一放大，做峰值标准化，**峰值上限 -1 dB，放大但不破音**（不许顶到 0 dB 削波）；她之后丢过来的配音文件同样处理
- 参考音：普通台词用该角色自己的 SELECT 类最长原音；**攻击、痛呼这类喊叫句必须用该角色自己的同类原音当参考**（拿温柔的问候音配喊杀句必糊）
- 自动质检三查，不合格自动换 seed / 降速重配（最多 4 次），仍不过就标出、保留成品等听审：
  1. 内容：ASR 回听转写与目标台词的相似度不低于 0.5（2 字以内的短句免检内容）
  2. 字速：不超过 4.2 字 / 秒
  3. 时长：3 字以上的短句不短于 1.30 秒
- 人工只听两类：每个新角色的第一条样音、被标出的条；决定只有三种：留、重配、去掉

## 佣兵文件夹对应（已核对，多为台词 + 命名推断）

| 游戏里叫 | 文件夹 | 备注 |
| --- | --- | --- |
| Harlequin | ARLECCHINO | 10 条 |
| Knight 进化线 | ARTHUR | 11 条，台词有 Excalibur / FOR CAMELOT；Sage King Arthur 约对应 WHITEARTHUR |
| Viking | VIKING | |
| Northern Viking | VIKINGC5 | 与 VIKING 两夹音频逐条完全相同，是同一套录音复制两份，靠耳朵分不出来 |
| Beast Trainer | BEASTMASTER | eng 7 条，名字直对的同义代号 |
| 卑弥呼 | HIMIKO | 名字直对；cn 残集里全 8 条都在，所以没配 |

## 待办

- ETERNITY 整批的听审决定还没做：144 条标出（涉及 57 个角色）、98 个角色的过检首条样音、另有 6 条纯拟译但质检过了的也要亲自听（SAE_SELECT3、VALKYRIE_MAGICBUF、WASHINGTONT_ATTACK1、WASHINGTONT_ATTACK5、SRHYEGA_SELECT1、MGWESTWITCHM_SELECT1）
- BUTLER、PROPHET、SPARTAN 三个角色全部条目都被标出，没有一条过检样音
- 旧的 fx 配音批（2026-10-26 停在 272/1110）是另一条线，不在本仓库范围内，不重开
