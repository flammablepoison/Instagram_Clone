# Instagram_Clone
import 'package:flutter/material.dart';
import 'package:bubble/bubble.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  //Open navigation menu listTile widget
  Widget listTileWidget(
      {@required icon,
      @required iconColor,
      @required text,
      @required textColor}) {
    return ListTile(
      leading: Icon(icon, color: iconColor),
      title: Text(text, style: TextStyle(color: textColor)),
      onTap: () {},
    );
  }

  @override
  Widget build(BuildContext context) {
    Widget drawerAppBar() {
      return Drawer(
        child: Container(
          child: ListView(
            children: [
              listTileWidget(
                  icon: Icons.settings,
                  iconColor: Colors.black,
                  text: 'Settings',
                  textColor: Colors.black),
              listTileWidget(
                  icon: Icons.group,
                  iconColor: Colors.black,
                  text: 'Form a group',
                  textColor: Colors.black),
              listTileWidget(
                  icon: Icons.wallpaper_outlined,
                  iconColor: Colors.black,
                  text: 'Chance wallpaper',
                  textColor: Colors.black),
            ],
          ),
        ),
      );
    }

    return MaterialApp(
        debugShowCheckedModeBanner: false,
        title: 'Flutter Demo',
        theme: ThemeData(
          primarySwatch: Colors.blue,
        ),
        home: SafeArea(
            child: Scaffold(
          endDrawer: drawerAppBar(),
          appBar: AppBar(
            iconTheme: IconThemeData(color: Colors.black),
            title: Row(
              children: [
                Text('Aile Bağları', style: TextStyle(color: Colors.black)),
              ],
            ),
            backgroundColor: Colors.white,
          ),
          body: const MyHomePage(),
        )));
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  //Yazının boş olup olmadığını göstermek
  bool isAllSpaces(String input) {
    String output = input.replaceAll(' ', '');
    if (output == '') {
      return true;
    }
    return false;
  }

  TextEditingController t1 = TextEditingController();
  Widget popupListTileWidget(
      {@required icon,
      @required iconColor,
      @required text,
      @required textColor}) {
    return ListTile(
      leading: Icon(icon, color: iconColor),
      title: Text(text, style: TextStyle(color: textColor)),
      onTap: () {},
    );
  }
  
  /*List popupMenuButton = <String>['Emojis','Chance keyboard','Gallery','Camera','Text style'];*/
  List mesajListesi = [];
  
  listeyeMesajEkle(String metin) {
    setState(
      () {
        if (isAllSpaces(t1.text) == true) {
        } else if (isAllSpaces(t1.text) == false) {
          mesajListesi.insert(0, metin);
          t1.clear();
        }
      },
    );
  }

  @override
  Widget build(BuildContext context) {
    //Message Buble
    Widget setMessageBalonu({@required indexnumarasi1}) {
      return Bubble(
        borderColor: Colors.black,
        borderWidth: 1.2,
        color: Colors.transparent,
        margin: BubbleEdges.fromLTRB(
            MediaQuery.of(context).size.width * 0.25, 10, 0, 0),
        nip: BubbleNip.rightBottom,
        alignment: Alignment.topRight,
        child: Text(
          mesajListesi[indexnumarasi1],
          textAlign: TextAlign.left,
          style: TextStyle(color: Colors.black),
        ),
      );
    }

    return Column(
      //mainAxisAlignment: MainAxisAlignment.end,
      children: [
        Flexible(
          child: Container(
            margin:
                EdgeInsets.fromLTRB(5, 0, 5, 10), //margin verildi istersen sil
            child: ListView.builder(
                reverse: true,
                itemCount: mesajListesi.length,
                itemBuilder: (context, int indexnumarasi) =>
                    setMessageBalonu(indexnumarasi1: indexnumarasi)),
          ),
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.spaceAround,
          children: [
            //TEXT İNPUT
            Container(
              alignment: Alignment.center,
              width: MediaQuery.of(context).size.width * 0.83,
              height: 36,
              decoration: BoxDecoration(
                  border: Border.all(color: Colors.black, width: 1.2),
                  borderRadius: BorderRadius.circular(30)),
              child: TextField(
                controller: t1,
                maxLines: 1,
                style: TextStyle(
                  color: Colors.black,
                  fontSize: 17,
                ),
                textAlignVertical: TextAlignVertical.center,
                decoration: InputDecoration(
                    filled: true,
                    border: OutlineInputBorder(
                        borderSide: BorderSide.none,
                        borderRadius: BorderRadius.all(Radius.circular(30))),
                    fillColor: Colors.transparent,
                    contentPadding: EdgeInsets.fromLTRB(20, 0, 20, 0),
                    hintText: 'Message',
                    hintStyle: TextStyle(color: Colors.black),
                    suffixIcon: 
                    //TEXTFİELD EXTRA PROPERTY ICON
                    PopupMenuButton(
                        shape: RoundedRectangleBorder(
                          side: BorderSide(color: Colors.black, width: 1.2),
                          borderRadius: BorderRadius.circular(10),
                        ),
                        padding: EdgeInsets.fromLTRB(0, 0, 0, 2),
                        icon: Icon(Icons.more_vert, color: Colors.black),
                        itemBuilder: (context) => [
                              PopupMenuItem(
                                child: popupListTileWidget(
                                    icon: Icons.emoji_emotions_outlined,
                                    iconColor: Colors.black,
                                    text: 'Emojis',
                                    textColor: Colors.black),
                              ),
                              PopupMenuItem(
                                child: popupListTileWidget(
                                    icon: Icons.keyboard_alt_outlined,
                                    iconColor: Colors.black,
                                    text: 'Change keyboard',
                                    textColor: Colors.black),
                              ),
                              PopupMenuItem(
                                child: popupListTileWidget(
                                    icon: Icons.image,
                                    iconColor: Colors.black,
                                    text: 'Gallery',
                                    textColor: Colors.black),
                              ),
                              PopupMenuItem(
                                child: popupListTileWidget(
                                    icon: Icons.camera_alt_outlined,
                                    iconColor: Colors.black,
                                    text: 'Camera',
                                    textColor: Colors.black),
                              ),
                              PopupMenuItem(
                                child: popupListTileWidget(
                                    icon: Icons.text_fields_outlined,
                                    iconColor: Colors.black,
                                    text: 'Text style',
                                    textColor: Colors.black),
                              ),
                            ])
                    //IconButton(onPressed: (){}, icon: Icon(Icons.more_vert,color: Colors.black,),padding: EdgeInsets.fromLTRB(0, 0, 0, 2),)

                    ),
              ),
            ),
            //SEND BUTTON
            Container(
              width: MediaQuery.of(context).size.width * 0.12,
              height: 36,
              margin: EdgeInsets.fromLTRB(0, 0, 0, 6),
              decoration: BoxDecoration(
                  borderRadius: BorderRadius.circular(80),
                  border: Border.all(color: Colors.black, width: 1.2)),
              child: ElevatedButton(
                  style: ButtonStyle(
                    backgroundColor:
                        MaterialStateProperty.all(Colors.transparent),
                  ),
                  onPressed: () {
                    listeyeMesajEkle(t1.text);
                  },
                  child: Icon(
                    Icons.send,
                    color: Colors.black,
                  )),
            )
          ],
        )
      ],
    );
  }
}
