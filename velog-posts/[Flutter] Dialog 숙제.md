<h3 id="생김새">생김새</h3>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/a9d733ab-2442-466a-bbf3-e60b2440481b/image.png" /></p>
<h3 id="코드">코드</h3>
<pre><code class="language-dart">import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(home: MyApp()));
}

class MyApp extends StatefulWidget {
  MyApp({super.key});

  @override
  State&lt;MyApp&gt; createState() =&gt; _MyAppState();
}

class _MyAppState extends State&lt;MyApp&gt; {
  var name = ['닭강정', '마라샹궈', '소불고기'];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          showDialog(
            context: context,
            builder: (context) {
              return Dialog(
                shape: RoundedRectangleBorder(borderRadius: BorderRadius.zero),
                child: Homework(),
              );
            },
          );
        },
      ),
      appBar: AppBar(),
      body: ListView.builder(
        itemCount: 3,
        itemBuilder: (context, i) {
          return ListTile(
            leading: Image.asset('grape.png'),
            title: Text(name[i]),
          );
        },
      ),
    );
  }
}

class Homework extends StatelessWidget {
  const Homework({super.key});

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: 300,
      child: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          spacing: 15,
          mainAxisSize: MainAxisSize.min,
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Contact',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            TextField(),
            Row(
              mainAxisAlignment: MainAxisAlignment.end,
              children: [
                TextButton(
                  onPressed: Navigator.of(context).pop,
                  child: Text('Cancel'),
                ),
                TextButton(
                  onPressed: Navigator.of(context).pop,
                  child: Text('OK'),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}</code></pre>