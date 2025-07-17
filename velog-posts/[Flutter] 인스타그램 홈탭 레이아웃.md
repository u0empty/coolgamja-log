<h3 id="생김새">생김새</h3>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/e4d29f60-9665-448b-a4b0-e1f325e1d423/image.png" /></p>
<p>정말 못생겼다</p>
<h3 id="코드body">코드(body)</h3>
<pre><code class="language-dart">body: [
  ListView.builder(
    itemCount: 3,
    itemBuilder: (context, i) {
      return Column(
        crossAxisAlignment: CrossAxisAlignment.center,
        children: [
          Image.asset(
            'assets/icecream.png',
          ),
          Padding(
            padding: const EdgeInsets.all(20),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.start,
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Row(
                  children: [
                    Text('좋아요 ', style: bold),
                    Text('100', style: bold),
                  ],
                ),
                Text('글쓴이'),
                Text('글내용'),
              ],
            ),
          ),
        ],
      );
    },
  ),
  Text('샵'),
][tab],</code></pre>