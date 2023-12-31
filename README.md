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

3. new TWEEN.Tween()で生成、いろいろ設定して、startで開始する。
```ts:App.tsx
  const tween = new TWEEN.Tween(ref.current.position)
                .to({x: 1, y: 3, z: 0,  rotation: 0}, 2000)
                .delay(1000)
                .easing(TWEEN.Easing.Elastic.InOut)
  const tweenrot = new TWEEN.Tween(ref.current.rotation)
                .to({x: Math.PI, y: 0, z: 0,  rotation: 0}, 2000)
                .easing(TWEEN.Easing.Elastic.InOut)
  const tweenBack = new TWEEN.Tween(ref.current.position)
                .to({x: 1, y: 1, z: 1, rotation: 0}, 3000)
                .easing(TWEEN.Easing.Elastic.InOut)
  tween.chain(tweenrot)
  tweenrot.chain(tweenBack)
  tweenBack.chain(tween)
  tween.start()
```

4. useEffectで初回startすると、動き続ける。デフォルト繰り返し？
to()に設定するrotationは値設定しても意味ないみたい。
移動させたいときは、new TWEEN.Tween()の引数に、ref.current.positionを設定して、
回転させたいときは、new TWEEN.Tween()の引数に、ref.current.rotationを設定する。
一度に移動させたいときは...？調査中。
