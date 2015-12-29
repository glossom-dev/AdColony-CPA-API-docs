AdColony CPA API 仕様書
=========================================

このドキュメントは、AdColony_Integration_Guide_ を日本語に翻訳したものです

.. _AdColony_Integration_Guide: ./AdColony_Integration_Guide.pdf

AdColony側のシステムと統合するために、インストールデータをAdColonyのCPA APIにポストバックする必要があります。

この資料は、ポストバックURLの詳細設定手順書です。

ポストバックURL設定
--------------------------------

アクション
^^^^^^^^^^^^^^^^^^^^^^^

::

   GET https://cpa.adcolony.com/on_user_action


必須パラメータ
^^^^^^^^^^^^^^^^^^^^^^^

api_key
  御社のプロダクトのユーザアクションを通知するためのAPI Keyです。
  API Keyが必要な方は tracking-support@adcolony.com までご連絡ください。

product_id
  iTunesにおけるアプリIDか Google Playにおけるbundle IDを指定してください
  
raw_advertising_id
  iOSのIDFA（MD5やSHA1などのハッシュ化はしないでください）

google_ad_id
  Android端末における広告ID（MD5やSHA1などのハッシュ化はしないでください）

任意パラメータ
^^^^^^^^^^^^^^^^^^^^^^^

adc_conversion
  インストールがAdColonyによる判定なのかどうかを識別するためのフラグ。
  1のときはAdColonyによるもの、0のときはそれ以外によるもの。
  このパラメータが空だった場合、CPA APIに送られてきた全てのインストールを取得する。

レスポンス
^^^^^^^^^^^^^^^^^^^^^^^

フォーマットはjsonで、成功した場合 '{status:true}' というjson文字列が返ります

リクエスト例
^^^^^^^^^^^^^^^^^^^^^^^

::

   GET https://cpa.adcolony.com/on_user_action?api_key=abc123def456&product_id=<prod_id>&raw_advertising_id=<idfa>&google_ad_id=<gaid>


トラッキングURL設定
--------------------------------

以下の変数とマクロが利用可能です

端末ID(必須項目)
^^^^^^^^^^^^^^^^^^^^^^^^

================== ================== ================== ====================================
変数               マクロ             プラットフォーム   説明
================== ================== ================== ====================================
IDFA               [IDFA]             iOS 6.0+           プライマリID for iOS
Google Ad ID       [GOOGLE_AD_ID]     Android            プライマリID for Android
================== ================== ================== ====================================

マクロ
^^^^^^^^^^^^^^^^^^^^^^^^

================== ===================== ===============================================
変数               マクロ                説明
================== ===================== ===============================================
Product ID         [PRODUCT_ID]          iTunesにおけるアプリIDかGoogle Payのbundle ID
App ID             [APP_ID]              SHA1でhashしたアプリID
Publisher ID       [PUBLISHER_ID]        SHA1でhashしたパブリッシャーID
キャンペーンID     [RAW_AD_CAMPAIGN_ID]  AdColonyキャンペーンID
キャンペーン名     [AD_CAMPAIGN_NAME]    AdColonyキャンペーン名
広告グループID     [RAW_AD_GROUP_ID]     AdColony広告グループID
広告グループ名     [AD_GROUP_NAME]       AdColony広告グループ名
クリエイティブID   [RAW_AD_CREATIVE_ID]  AdColony広告クリエイティブID
クリエイティブ名   [AD_CREATIVE_NAME]    AdColony広告クリエイティブ名
プラットフォーム   [PLATFORM]            iOS/Android
OSバージョン       [OS_VERSION]          iOS 6.0.1などのOSバージョン
端末タイプ         [DEVICE_MODEL]        iPad, iPhone, iPodなどの端末モデル
国                 [COUNTRY]             端末の国コード
IP                 [IP_ADDRESS]          端末のIPアドレス
言語               [LANGUAGE]            端末言語設定
================== ===================== ===============================================

※ Product IDはクリックURLにもつけておくことが望ましい

トラッキングURL 例
^^^^^^^^^^^^^^^^^^^^^^^

::

   iOS
   http://www.yoururl.com/?idfa=[IDFA]&prod_id=[PRODUCT_ID]&siteid=[APP_ID]
   Android
   http://www.yoururl.com/?gaid=[GOOGLE_AD_ID]&prod_id=[PRODUCT_ID]&siteid=[APP_ID]
