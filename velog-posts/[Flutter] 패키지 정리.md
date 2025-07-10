<h2 id="permission_handler"><a href="https://pub.dev/packages/permission_handler">permission_handler</a></h2>
<p>유저에게 앱 권한(카메라, 위치, ..)을 요청할 때 사용</p>
<h3 id="import">import</h3>
<p><code>import 'package:permission_handler/permission_handler.dart';</code></p>
<h3 id="pubspecyaml">pubspec.yaml</h3>
<pre><code class="language-dart">dependencies:
  flutter:
    sdk: flutter
  permission_handler: ^12.0.1</code></pre>
<h3 id="androidmanifestxml">Android.manifest.xml</h3>
<pre><code class="language-dart">&lt;uses-permission android:name=&quot;android.permission.READ_CONTACTS&quot;/&gt;
&lt;uses-permission android:name=&quot;android.permission.WRITE_CONTACTS&quot;/&gt;</code></pre>
<h3 id="example">example</h3>
<pre><code class="language-dart">getPermission() async {
  var status = await Permission.contacts.status;

  if (status.isGranted) {
    print('허락됨');
  } else if (status.isDenied) {
    print('거절됨');
    await Permission.contacts.request();
  } else if (status.isPermanentlyDenied) {
    openAppSettings();
  }
}

// (생략)

IconButton(
  onPressed: () {
    getPermission();
  },
  icon: Icon(Icons.contacts),
),</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/371dd51f-b87d-4d4a-8bf5-13e7494ff257/image.png" /></p>
<h2 id="flutter_contacts"><a href="https://pub.dev/packages/flutter_contacts">flutter_contacts</a></h2>
<p>유저에게 연락처 권한 요청할 때 사용</p>
<h3 id="import-1">import</h3>
<p><code>import 'package:flutter_contacts/flutter_contacts.dart';</code></p>
<h3 id="pubspecyaml-1">pubspec.yaml</h3>
<pre><code class="language-dart">dependencies:
  flutter_contacts: ^1.1.9+2</code></pre>
<h3 id="example-1">example</h3>
<pre><code class="language-dart">// 연락처 불러오기
Future&lt;void&gt; loadContacts() async {
  if (await Permission.contacts.request().isGranted) {
    List&lt;Contact&gt; contacts = await FlutterContacts.getContacts(withProperties: true);
    setState(() {
      name = contacts;
    });
  }
}

// 연락처 추가하기
Future&lt;void&gt; addContact(String newName, String newNumber) async {
  final newContact = Contact()
    ..name.first = newName
    ..phones = [Phone(newNumber)];
  await newContact.insert();
}

// 연락처 까보기
ListTile(
  title: Text(contact.displayName),
  subtitle: Text(contact.phones.isNotEmpty ? contact.phones[0].number : ''),
)</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/b1f1b692-ece4-40da-9583-a6c4beb8b151/image.png" /></p>