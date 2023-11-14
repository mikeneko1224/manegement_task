# 技術課題

# ターゲット
約10名~20名程度のパン屋の店長

# 背景
店長の業務
・食品の売れ行きやお客様がよく来る時間帯の分析
・シフトの作成
　→・紙で従業員に提出して貰うため、手で記入
 　・もし、シフトを組む際に、この時間に何人欲しいやイベントがある日に、シフトに入って貰えないかを従業員に声をかける事もある)
・従業員の勤怠は、タイムカードで管理(手入力)
・上の人に従業員の勤怠情報や売り上げなどを作成し、CSVファイルでメールに送る。
・従業員に教えたり、仕事上の相談にのる。


# 課題
1. シフト表の作成
　・出勤できる日に偏りがあり、来てほしい日にあまり人が入っておらず、あまり人数が必要ない日に出勤できる人が多いなどがある。
  　→出勤できないかを頼むこともあり
  ・紙でシフトを提出するため、一度パソコンに入力してから、シフトを考える。
  ・効率よく日による必要な人数というのを設定したい。
2. 勤怠管理
　タイムカードの情報をもとに、手入力を行う
3. 上の方に、売り上げ成績をCSVファイルで提出
4. 従業員の育成
　→新人に仕事など教えたいが、上記の仕事で時間が取れず、難しい
  →新作や、新しい取り組みなどの相談をじっくりと行いたいが厳しい


# 提案
1. 人数が不足している日付には、背景に色をつける。
   →従業員はそれを見て、入れるかを考えてもらうようにする
   編集したい日付をクリックするだけで変更できるようにする
   編集したら、シフトを反映
   機械学習で日付によって必要な人数を予測
2. 打刻をデータベースに保存することで、記録を残す。
   →なるべく、従業員が打刻忘れを無くすために、ボタンをクリックするだけにする
   (従業員の打刻忘れの原因：打刻を日付や出勤、退勤などの種類選択などをするのが面倒、ギリギリの出勤や退勤後にすぐに遊びたいなどによって、後回しにする)
   　→店長が勤怠管理の不正の確認や打刻忘れによる連絡などをなるべく抑えて、店長の業務を減らす。
3. bootstrapでCSVに変換して、提出が出来るかも
4. シフト表の作成、勤怠管理などの時間短縮が行えば、時間が出来、対応できるようになる


# 機能(数字が小さいほど、実装したい機能)
1. 人数が不足している日付の背景をピンクに変更
   →今回は、10:00~14:00の時間にお客様が良く来ることを想定し、必ずアルバイトやパートの従業員には10:00~14:00の時間に一人が入るように設定
   　→10:00~14:00に一人でもシフトを入れると、背景が白色
      10:00~14:00にシフトが入っていないと、背景が赤色に表示
2. 店長のシフト編集は日付をクリックした際に、選択形式(×、10:00~14:00など)で変更可能
   →bootstrapで画面遷移をせずに変更画面を表示するようにする
3. 打刻を出勤ボタン、退勤ボタン、休憩開始ボタン、休憩終了ボタンをそれぞれ押すと、データベースには、従業員のID、勤怠の種類(出勤や退勤など)、日付(2023-11-13と表記)、時間(08:00:00と表記)が記載される。 


# 開発環境
・windows 10 Home  
 
・laravel 10.30.1  

・next.js 14.0.2  

# データベース
　xammp　8.2.4

# データベースの中
●データベース名：staff
●テーブル
　・add_time(勤怠の時間を保存)　→　列名:name(idを記載)、text(勤怠の種類)、date(日付)、time(時間)
  ・staffname(ログイン時のメンバーIDと名前)　→　列名:id(idを記載)、name(名前)
  ・shifttable(シフト提出の日付と時間)　→　列名:id(key)、number(ID)、date(日付)、time(時間)
