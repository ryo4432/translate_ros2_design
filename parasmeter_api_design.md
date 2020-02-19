# ROSにおけるパラメータAPIの設計

この記事は，ROS2におけるパラメータとやり取りするためのインターフェイスの設計案です。我々はここでシステム設計を明記することに焦点を当て，実装については明記しないままにします。

# 背景
ROS1では，パラメータは「ブラックボードパターン」で実現されており，すべてのノードから制限のなく読み書きのアクセスが可能だった。このデータモデルは多くのケースで有用であることを証明したが，コントロールや所有権の欠如において問題があることを示す多くのケースがあった。よく言われている欠点の1つに，ドライバーのパラメータ設定がある。dynamic_reconfigureと呼ばれるツールはこのユースケースを対処するために開発された。dynamic_reconfigureは，ほかのノードのパラメータとやり取りするために，サービスベースのインターフェイスを提供した。

## そのほかのリソース
ROS2のためのパラメータ設計過程に関するそのほかのリソースは以下。
- Gonzalo’s research on parameters.
    - Discussion: https://groups.google.com/forum/#!topic/ros-sig-ng-ros/YzCmoIsN0o8 and https://groups.google.com/forum/#!searchin/ros-sig-ng-ros/parameter/ros-sig-ng-ros/fwDBcei5Ths/L6ORPfjUDXYJ
    - Prototype: https://github.com/abellagonzalo/dynamic_config
    - Final Notes: http://wiki.ros.org/sig/NextGenerationROS/Parameters
- Thibault’s nodeparam draft REP: https://github.com/tkruse/rep/blob/nodeparam/nodeparam-REP.rst


# 理想的なシステム
