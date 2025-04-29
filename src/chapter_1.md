# Chapter 1

## test1
## test2

The `mdbook init` command will create a new directory containing an empty book for you to get started.
Give it the name of the directory that you want to create:


download on the [GitHub Releases page][releases]
[releases]: https://github.com/rust-lang/mdBook/releases


For example:
- `MDBOOK_foo` -> `foo`
- `MDBOOK_FOO` -> `foo`

So by setting the `MDBOOK_BOOK__TITLE` environment variable you can override the
book's title without needing to touch your `book.toml`.[^1]
[^1]: https://web.archive.org/web/20240124025806/https://www.infoq.com/podcasts/software-architecture-hard-parts/

> **Note:** To facilitate setting more complex config items, the value of an
> environment variable is first parsed as JSON, falling back to a string if the
> parse fails.
>


| Icon | Name |
|------|-------------|
| <i class="fa fa-bars"></i> | fa-bars |
| <i class="fa fa-check-square"></i> | fa-check-square |
| <i class="fa fa-paint-brush"></i> | fa-paint-brush |
| <i class="fa fa-search"></i> | fa-search |
| <i class="fa fa-print"></i> | fa-print |
| <i class="fa fa-github"></i> | fa-github |
| <i class="fa fa-edit"></i> | fa-edit |
| <i class="fa fa-spinner fa-pulse fa-3x fa-fw"></i> | fa-spinner |
|```rust let a = String::from("abc");```<br>```println!("{}", a);```|aaa|

```rust
let s = String::from("❌⭕👀✅❎❗❓🟢🔴");
println!("{}", s);
```

```sh
mdbook init my-first-book
```

```text
hello world
```

😀😁😂🤣😃😄😅😆😉😊😋😎😍😘😗😙😚🙂🤗🤔😐😑😶🙄😏😣😥😮🤐😯😪😫😴😌🤓😛😜😝🤤😒😓😔😕🙃🤑😲🙁😖😞😟😤😢😭😦😧😨😩😬😰😱😳😵😡😇🤡🤥😷🤒🤕🤢🤧😈👿👹👺💀👻👽👾🤖💩😺😸😹😻😼😽🙀😿😾🙈🙉🙊👦👧👨👩👴👵👶👼👮💂👷👳👱🎅🤶👸🤴👰🤵🤰👲🙍🙎🙅🙆💁🙋🙇🤦🤷💆💇🚶🏃💃🕺👯👤👥🤺🏇🏂🏄🚣🏊🚴🚵🤸🤼🤽🤾🤹👫👬👭💏💑👪💪🤳👈👉👆👇🤞🖖🤘🤙✋👌👍👎✊👊🤛🤜🤚👋👏👐🙌🙏🤝💅👂👃👣👀👅👄💋💘💓💔💕💖💗💙💚💛💜🖤💝💞💟💌💤💢💣💥💦💨💫💬💭👓👔👕👖👗👘👙👚👛👜👝🎒👞👟👠👡👢👑👒🎩🎓📿💄💍💎 

 

🐵🐒🦍🐶🐕🐩🐺🦊🐱🐈🦁🐯🐅🐆🐴🐎🦌🦄🐮🐂🐃🐄🐷🐖🐗🐽🐏🐑🐐🐪🐫🐘🦏🐭🐁🐀🐹🐰🐇🦇🐻🐨🐼🐾🦃🐔🐓🐣🐤🐥🐦🐧🦅🦆🦉🐸🐊🐢🦎🐍🐲🐉🐳🐋🐬🐟🐠🐡🦈🐙🐚🦀🦐🦑🦋🐌🐛🐜🐝🐞🦂💐🌸💮🌹🥀🌺🌻🌼🌷🌱🌲🌳🌴🌵🌾🌿🍀🍁🍂🍃 

 

🍇🍈🍉🍊🍋🍌🍍🍎🍏🍐🍑🍒🍓🥝🍅🥑🍆🥔🥕🌽🥒🍄🥜🌰🍞🥐🥖🥞🧀🍖🍗🥓🍔🍟🍕🌭🌮🌯🥙🥚🍳🥘🍲🥗🍿🍱🍘🍙🍚🍛🍜🍝🍠🍢🍣🍤🍥🍡🍦🍧🍨🍩🍪🎂🍰🍫🍬🍭🍮🍯🍼🥛☕🍵🍶🍾🍷🍸🍹🍺🍻🥂🥃🍴🥄🔪🏺 

 

 

🌍🌎🌏🌐🗾🌋🗻🏠🏡🏢🏣🏤🏥🏦🏨🏩🏪🏫🏬🏭🏯🏰💒🗼🗽⛪🕌🕍🕋⛲⛺🌁🌃🌄🌅🌆🌇🌉🌌🎠🎡🎢💈🎪🎭🎨🎰🚂🚃🚄🚅🚆🚇🚈🚉🚊🚝🚞🚋🚌🚍🚎🚐🚑🚒🚓🚔🚕🚖🚗🚘🚙🚚🚛🚜🚲🛴🛵🚏⛽🚨🚥🚦🚧🛑⚓⛵🛶🚤🚢🛫🛬💺🚁🚟🚠🚡🚀🚪🛌🚽🚿🛀🛁⌛⏳⌚⏰🕛🕧🕐🕜🕑🕝🕒🕞🕓🕟🕔🕠🕕🕡🕖🕢🕗🕣🕘🕤🕙🕥🕚🕦🌑🌒🌓🌔🌕🌖🌗🌘🌙🌚🌛🌜🌝🌞⭐🌟🌠⛅🌀🌈🌂☔⚡⛄🔥💧🌊 

 

🎃🎄🎆🎇✨🎈🎉🎊🎋🎍🎎🎏🎐🎑🎀🎁🎫🏆🏅🥇🥈🥉⚽⚾🏀🏐🏈🏉🎾🎱🎳🏏🏑🏒🏓🏸🥊🥋🥅🎯⛳🎣🎽🎿🎮🎲🃏🀄🎴 

 

🔇🔈🔉🔊📢📣📯🔔🔕🎼🎵🎶🎤🎧📻🎷🎸🎹🎺🎻🥁📱📲📞📟📠🔋🔌💻💽💾💿📀🎥🎬📺📷📸📹📼🔍🔎🔬🔭📡💡🔦🏮📔📕📖📗📘📙📚📓📒📃📜📄📰📑🔖💰💴💵💶💷💸💳💹💱💲📧📨📩📤📥📦📫📪📬📭📮📝💼📁📂📅📆📇📈📉📊📋📌📍📎📏📐🔒🔓🔏🔐🔑🔨🔫🏹🔧🔩🔗💉💊🚬🗿🔮🛒 

 

 

🏧🚮🚰♿🚹🚺🚻🚼🚾🛂🛃🛄🛅🚸⛔🚫🚳🚭🚯🚱🚷📵🔞🔃🔄🔙🔚🔛🔜🔝🛐🕎🔯♈♉♊♋♌♍♎♏♐♑♒♓⛎🔀🔁🔂⏩⏪🔼⏫🔽⏬🎦🔅🔆📶📳📴📛🔰🔱⭕✅❌❎➕➖➗➰➿❓❔❕❗🔟💯🔠🔡🔢🔣🔤🆎🆑🆒🆓🆔🆕🆖🆗🆘🆙🆚🈁🈶🈯🉐🈹🈚🈲🉑🈸🈴🈳🈺🈵◽◾⬛⬜🔶🔷🔸🔹🔺🔻💠🔘🔲🔳⚪⚫🔴🔵 

 

🏁🚩🎌🏴 