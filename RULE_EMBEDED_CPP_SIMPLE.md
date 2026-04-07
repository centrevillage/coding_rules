# せんとれ式C++コーディング規約（シンプル版）

## 禁止 (MUST NOT)

下記のキーワードは使用不可とする。

- アクセス指定子の `private/public/protected/friend`
- 仮想関数指定の `virtual`
- `class`
- 例外の `throw/try/catch`

構造体のメンバーは利用者に対してなにも隠蔽ができない。それらは関数同様のインタフェースとして注意深く設計することを推奨する。
キャッシュ変数などの利用者が意識すべきでないメンバー変数については、アクセス指定の代わりに、変数名の先頭にアンダースコア `_` をつけることを推奨する(例: `_temp`)。

同様に、利用者が注意を払うべきでないメンバー関数についても先頭に `_` を指定することを推奨する(例 `void _internalAction();`)。

C++において例外を適切に使うのは難しく、利用にあたっては多少のオーバーヘッドを許容しなければならない。 関数のエラー通知は戻り値にエラーコードを渡すなどの代替手段を取ること。

## 非推奨 (SHOULD NOT)

下記の機能は非推奨とし、真に必要な場合以外は使うべきではない。

- コンストラクタ/デストラクタ/コピーコンストラクタ/ムーブコンストラクタ

コンストラクタによるメンバ変数初期化の代替としては、下記のいずれかの手段を推奨する。

- void init() 等の初期化用メンバ関数
- static Hoge newHoge() 等の構造体のインスタンスを返す static 関数

## ネーミングルール

### ファイル名

- `snake_case` を使用する（例: `app_audio.hpp`, `looper_model.cpp`, `memory_manager.hpp`）
- 外部に公開しない内部用ヘッダは先頭に `_` をつける（例: `_app_ram_stm32.hpp`, `_app_ram_test.hpp`）
- C++ヘッダは `.hpp`、C++ソースは `.cpp`、Cソースは `.c` を使用する

### 構造体名・型名

- `PascalCase` を使用する（例: `LooperModel`, `AppAudio`, `MemoryManager`, `AppModeBase`）
- 型エイリアス (`using` / `typedef`) も同様に `PascalCase`（例: `AudioCallback`, `AppMuxIO`, `TimerCls`）

### enum class

- 型名は `PascalCase`（例: `EventId`, `AppBtnId`, `SyncSrc`）
- 値は `camelCase`（例: `changeStep`, `masterTransmit`, `slaveReceive`）

### メンバ関数

- `camelCase` を使用する（例: `init()`, `processAudio()`, `assignArea()`, `setLed()`, `isOn()`）
- 内部用メンバ関数は先頭に `_` をつける（「禁止」の項を参照）

### メンバ変数

- `snake_case` を使用する（例: `wet_balance`, `current_speed`, `free_area_count`）
- 内部用メンバ変数は先頭に `_` をつける（例: `_buf`, `_is_start`）（「禁止」の項を参照）

### フリー関数（非メンバ関数）

- `snake_case` を使用する（例: `current_tick()`, `sec_to_tick()`, `delay_tick()`, `i32_to_float()`）

### グローバル変数

- `snake_case` を使用する（例: `app_audio`, `looper_model`, `memory_manager`）

### 定数

- `constexpr` 定数は `snake_case` を使用する（例: `track_size`, `audio_ch_size`, `buffer_size`）
- マクロ定数およびマクロ的な `inline constexpr` 定数（ハードウェア定義等）は `UPPER_SNAKE_CASE` を使用する（例: `AUDIO_BLOCK_SIZE`, `DMA_BUFFER_MEM_SECTION`）

