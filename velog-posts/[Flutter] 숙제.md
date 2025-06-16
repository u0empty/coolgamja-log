<h3 id="만들다만거-아니고-다-만든거">만들다만거 아니고 다 만든거</h3>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/879ac05d-ae01-4b64-8596-467d21958901/image.png" /></p>
<h3 id="코드">코드</h3>
<pre><code class="language-dart">import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Row(
            children: [Text('금호동3가'), Icon(Icons.keyboard_arrow_down)],
          ),
          actions: [
            IconButton(icon: Icon(Icons.search), onPressed: () {}),
            IconButton(icon: Icon(Icons.menu), onPressed: () {}),
            IconButton(
              icon: Icon(Icons.notifications_outlined),
              onPressed: () {},
            ),
          ],
        ),
        body: SizedBox(
          height: 110,
          width: double.infinity,
          child: Row(
            mainAxisAlignment: MainAxisAlignment.start,
            children: [
              SizedBox(width: 10),
              Image.asset(
                'grape.png',
                height: 110,
                width: 110,
                fit: BoxFit.cover,
              ),
              SizedBox(width: 10),
              Flexible(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.start,
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(
                      '당근마켓 숙제하는 저 팝니다 쌉니다 싸요 단돈 이십일만원 다시는 오지 않을 가격',
                      style: TextStyle(
                        fontWeight: FontWeight.bold,
                        fontSize: 15,
                      ),
                    ),
                    Text(
                      '분당구 구미동, 끌올 10분 전',
                      style: TextStyle(fontSize: 12, color: Colors.grey),
                    ),
                    Text(
                      '210,000원',
                      style: TextStyle(fontWeight: FontWeight.bold),
                    ),
                    Row(
                      mainAxisAlignment: MainAxisAlignment.end,
                      children: [
                        Icon(Icons.favorite_border, size: 15),
                        SizedBox(width: 3),
                        Text('26'),
                        SizedBox(width: 10),
                      ],
                    ),
                  ],
                ),
              ),
              SizedBox(width: 10),
            ],
          ),
        ),
      ),
    );
  }
}</code></pre>