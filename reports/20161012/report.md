##解答  
rubyによるプロファイルを行った．  
ruby -r profile ./bin/trema run ./lib/cbench.rb によりプロファイルを実行した．  
コントローラを起動した後，./bin/cbench --port 6653 --switches 1 --loops 10 --ms-per-test 10000 --delay 1000 --throughput を行った．  
結果のうち，ボトルネックとなっている要素は以下であった．  
```
  %   cumulative   self              self     total  
 time   seconds   seconds    calls  ms/call  ms/call  name  
155.69   187.17    187.17        2 93585.00 93585.00  IO.select  
 77.85   280.76     93.59        2 46795.00 46795.00  Thread#join  
 77.84   374.34     93.58        2 46790.00 46790.00  TCPServer#accept  
```
![IO.selectについて](http://www.geekpage.jp/programming/ruby-network/select-0.php)  
![TCPServer#acceptについて](https://docs.ruby-lang.org/ja/latest/class/TCPServer.html)  
Thread#joinについてはよく分からなかった．  
