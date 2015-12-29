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

:api_key: 御社のプロダクトのユーザアクションを通知するためのAPI Keyです。
          API Keyが必要な方は tracking-support@adcolony.com までご連絡ください。
:product_id: iTunesにおけるアプリIDか Google Playにおけるbundle IDを指定してください
:raw_advertising_id: iOSのIDFA（MD5やSHA1などのハッシュ化はしないでください）
:google_ad_id: Android端末における広告ID（MD5やSHA1などのハッシュ化はしないでください）

任意パラメータ
^^^^^^^^^^^^^^^^^^^^^^^

:adc_conversion: インストールがAdColonyによる判定なのかどうかを識別するためのフラグ。
                 1のときはAdColonyによるもの、0のときはそれ以外によるもの

                 このパラメータが空だった場合、CPA APIに送られてきた全てのインストールを取得する

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


