1. bind 함수의 정체?
callback 함수로 어떤 객체의 메서드를 전달하게 되면, 더 이상 그 객체의 정보는 남아있지 않음.
이 이유에 대해서는 객체의 메서드의 접근해서, 객체의 정보까지 가져오는게 아니고 메서드만 복사해서 가져오는 것이 이유라고 생각함.
예를 들어, requestAnimationFrame(this.animate); 로 App의 animate 메서드를 넘기면 animate 메서드 코드 내부에서는
this 를 App 객체가 아닌 window 같은 전역 객체로 인식하게 됨. 이것이 그에 대한 근거로 보임. 
이거를 막기 위한 것이 바인딩(binding).
이놈을 사용하면 원하는 객체를 callback 함수에 넘겨줄 수 있음.
requestAnimationFrame(this.animate.bind(this)); 처럼 App 객체를 animate 메서드에 넘겨줌.

2. 레티나 디스플레이가 뭐길래 저런 작업을 해주어야 하는걸까?
레티나 디스플레이는 보통 디스플레이보다 픽셀 개수가 4배나 많음 (면적 기준. 가로 2배 * 세로 2배) 
따라서 캔버스의 픽셀 사이즈를 가로 세로 각각 2배씩 늘려주고, 캔버스 내부 컨텍스트의 크기를 2배로 확대시키면
레티나 디스플레이에서 작게 보이는 현상이 없어짐.