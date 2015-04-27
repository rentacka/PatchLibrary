# PatchLibrary

C++ ソースの変更を実行中のプログラムに反映させるライブラリ＆ツールです。  
主な用途として、プラグイン (DLL) の開発中にホストプログラムを再起動することなくプラグインを更新する、といったものを想定しています。  

Test 以下には Unity のプラグインを実行中に更新する簡単なテストプロジェクトが含まれています。  
TestUnityPlugin プロジェクトはビルドイベント (ビルド後イベント) でこのツールを呼び、Unity.exe に対して変更を適用しています。  

正確には、このツールは実行中のプロセスがロードしている DLL の関数を差し替える、ということをします。  
DLL Injection を用いて対象プロセスに新しい DLL をロードさせ、旧 DLL が export している関数のテーブルを新しい DLL の関数へ書き換えることで、更新を実現しています。  
このため、ネイティブコードの dll であれば C++ に限らず変更を適用できます。また、新しい DLL で新規に追加された export 関数はホストプログラムは認識できません。こういうケースでは再起動が必要になります。  

より技術的な詳細に興味があれば、以下のプロジェクトや blog 記事が参考になると思われます。   
https://github.com/i-saint/DynamicPatcher (本ツールはこれの簡易版的なものです)  
http://i-saint.hatenablog.com/entry/2013/06/06/212515  