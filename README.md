# react-tweenjs001
React+TypeScriptなWebアプリで、Tweenしてみた001。(移動と回転)

![image](https://github.com/aaaa1597/react-tweenjs001/assets/27885482/e5a5334e-d82e-4e87-86e9-7bc109681d42)

# ポイント
1. TWEENをimportする。
```ts:App.tsx
import TWEEN from '@tweenjs/tween.js'
```
2. Tween関数コンポーネントを作って、<Tween />タグを埋め込む。
```ts:App.tsx
const Tween = () => {
  useFrame(() => {
    TWEEN.update()
  })
  return(<></>)
}
～略～
   <Tween />
```

3. useEffectで初回startすると、動き続ける。デフォルト繰り返し？
to()に設定するrotationは値設定しても意味ないみたい。
移動させたいときは、new TWEEN.Tween()の引数に、ref.current.positionを設定して、
回転させたいときは、new TWEEN.Tween()の引数に、ref.current.rotationを設定する。
一度に移動させたいときは...？調査中。
