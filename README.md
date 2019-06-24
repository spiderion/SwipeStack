# swipe_stack

Swipe stack flutter.

- [swipe_stack](#swipestack)
  - [Screenshot](#Screenshot)
  - [Installation](#Installation)
  - [Usage](#Usage)
  - [Manuel Usage](#Manuel-Usage)

## Screenshot

![](https://raw.githubusercontent.com/gmetekorkmaz/images/master/swipe-stack/swipe.jpg)
![](https://raw.githubusercontent.com/gmetekorkmaz/images/master/swipe-stack/left.jpg)
![](https://raw.githubusercontent.com/gmetekorkmaz/images/master/swipe-stack/right.jpg)
![](https://raw.githubusercontent.com/gmetekorkmaz/images/master/swipe-stack/top.jpg)
![](https://raw.githubusercontent.com/gmetekorkmaz/images/master/swipe-stack/bottom.jpg)

[Youtube Video](https://www.youtube.com/watch?v=vWttY4jWa7k)

## Installation

Add 

```bash
swipe_stack : ^latest_version
```
to your pubspec.yaml.

## Usage

| Parameter | Default | Description |
| --------- | ------- | ----------- |
| maxAngle  | 35 | Maximum rotation value. Must be int between 0 and 360 |
| threshold | 30  | Manual swipe is canceled when the card is dragged less than threshold. Must be int between 1 and 100 |
| stackFrom | StackFrom.None | Stack type. Must be one of StackFrom.Left, StackFrom.Right, StackFrom.Top, StackFrom.Bottom, StackFrom.None |
| visibleCount | 2 | Number of objects to display. Must int and at least 2 |
| translationInterval | 0 | Distance between objects. Must be positive integer |
| scaleInterval | 0 | Decreasing scale value. Must be positive double |
| animationDuration | Duration(milliseconds: 200) | Animation duration |
| historyCount | 1 | Number of objects to keep in the history. Must be positive integer |
| padding | EdgeInsets.symmetric(vertical: 20, horizontal: 25) | Main container padding |

```bash
SwipeStack(
    children: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map((int index) {
        return SwiperItem(
            builder: (SwiperPosition position, double progress) {
                return Material(
                    elevation: 4,
                    borderRadius: BorderRadius.all(Radius.circular(6)),
                    child: Container(
                        decoration: BoxDecoration(
                            color: Colors.white,
                            borderRadius: BorderRadius.all(Radius.circular(6)),
                        ),
                        child: Column(
                            mainAxisAlignment: MainAxisAlignment.center,
                            children: <Widget>[
                                Text("Item $index", style: TextStyle(color: Colors.black, fontSize: 20)),
                                Text("Progress $progress", style: TextStyle(color: Colors.blue, fontSize: 12)),
                            ],
                        )
                    )
                );
            }
        );
    }).toList(),
    visibleCount: 3,
    stackFrom: StackFrom.Top,
    translationInterval: 6,
    scaleInterval: 0.03,
    onEnd: () => debugPrint("onEnd"),
    onSwipe: (int index, SwiperPosition position) => debugPrint("onSwipe $index $position"),
    onRewind: (int index, SwiperPosition position) => debugPrint("onRewind $index $position"),
)
```

## Manuel Usage

```bash
final GlobalKey<SwipeStackState> _swipeKey = GlobalKey<SwipeStackState>();
```

```bash
SwipeStack(
    key: _swipeKey,
    ...,
)
```

```bash
    _swipeKey.currentState.swipeLeft();
    _swipeKey.currentState.swipeRight();
    _swipeKey.currentState.rewind();
```