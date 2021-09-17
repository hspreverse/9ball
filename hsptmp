#include "hgimg.as"

	;	3Dシーン表示サンプル
	;	(パレットモード)
	;


	;	ウインドゥサイズの設定
	;
	screen 0,640,480,1
;	screen 0,320,240,1
	cls 4

	;	初期設定
	;
	hgini
	onexit *owari

	;	テクスチャフォント表示の準備
	;
	setfont 16,16,12,1	; font Tex select(cx,cy,px,mode)
	texload "fontchr.bmp"	; フォントテクスチャの登録

	;	MXファイルオブジェクトを登録(背景)
	;
	mxload "room"			; モデルファイル読み込み
	regobj bgchr,stat,OBJ_GROUND	; (変数statにモデルIDが返される)
	selpos bgchr
	objsetf3 0.0f, 10.0f, 0.0f

	;	MXファイルオブジェクトを登録(キャラ)
	;
	mxload "9ball"		; モデルファイル読み込み
	regobj mychr,stat	; (変数statにモデルIDが返される)
	setcoli	mychr,1,2	; コリジョン設定(自分=1/敵=2)
	selscale mychr
	objsetf3 0.025f, 0.025f, 0.025f
	selpos mychr
	objsetf3 0.0f, 0.0f, 0.0f

	;	3Dスプライトの登録
	;
	setuv 0,0,99,99
	setsizef 8.0f, 8.0f
	addplate ball,1
	texload "ball2.bmp"	; テクスチャの登録
	regobj enemy,ball,OBJ_TREE
	setcoli	enemy,2,0
	selpos enemy
	objsetf3 -20.0f, 0.0f, 0.0f
	regobj enemy,ball,OBJ_TREE
	setcoli	enemy,2,0
	selpos enemy
	objsetf3 20.0f, 0.0f, 0.0f

	;	パレットをコピー
	;
	gsel 0
	palcopy 3

	;	カメラ位置設定
	;
	cammode CAM_MODE_LOOKAT		; カメラ注視モード
	selcpos
	objsetf3 0.0f, -20.0f, 80.0f	; カメラ座標

*main
	;	カメラ&自キャラ移動
	selpos mychr
	objgetfv fv
	
	stick k,127
	if k&128 : goto *owari		; [ESC]で終了
	selang mychr
	if k&1 : objaddf1 1,-0.05f
	if k&16 {			; 前進
		objgetfv fv2
		fvdir fv2,0.0f,0.0f,3.0f
		fvadd fv,fv2.0,fv2.1,fv2.2
	}
	if k&4 : objaddf1 1,0.05f
	if k&2 {			; 前進
		objgetfv fv2
		fvdir fv2,0.0f,0.0f,1.0f
		fvadd fv,fv2.0,fv2.1,fv2.2
	}
	if k&8 {			; 後退
		objgetfv fv2
		fvdir fv2,0.0f,0.0f,-1.0f
		fvadd fv,fv2.0,fv2.1,fv2.2
	}
	fvmin fv, -50.0f, -50.0f, -50.0f ; 下限
	fvmax fv, 50.0f, 50.0f, 50.0f	 ; 上限

	selpos mychr
	objsetfv fv
	selcint
	objsetfv fv			; 自キャラを注視点に

	;	当たり判定
	;
	getcoli a,mychr,8.0f
	if a!=-1 {
		selpos a:objaddf1 1,-1.5f
	}

	;	描画メイン
	;
	hgdraw				; 描画処理
	getsync t1,0			; 前回からの負荷を取得
	fprt "HGIMG Test",8,8
	fprt "SYNC:"+t1,8,24
	hgsync 14			; 処理落ちしてなければ描画

	goto *main

*owari
	hgbye
	end

