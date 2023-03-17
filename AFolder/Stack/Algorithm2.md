***** 유효한 괄호쌍
<p>입력된 괄호 값들이 모두 쌍이 맞게 올바른지를 판단해 모두 쌍이 맞으면 true 그렇지 않으면 false를 출력하세요. </p>

const isValid = (str) => {
		// 최초 입력값이 빈 값이라면 유효하지 않은 괄호쌍으로 간주합니다.
		if (str.length === 0) return false;

    // 각각의 여는 괄호에 알맞는 닫는 괄호를 매칭시키기 위한 괄호맵 생성.
    const braketsMap = {
        '(': ')',
        '[': ']',
        '{': '}'
    };

    const arr = str.split('');
    const stack = [];

    for (let i = 0; i < arr.length; ++i) {
        // 1. 여는 괄호 -> stack에 push해야 하는 케이스
        if (arr[i] === '(' || arr[i] === '[' || arr[i] === '{') {
            stack.push(arr[i]);
        } else {
            // 2. 닫는 괄호 -> stack에서 pop해야 하는 케이스

            // 먼저 현재 stack의 가장 위에 위치한 괄호를 확인하고
            const lastElementOfStack = stack[stack.length - 1];
            
            // 지금 처리해야하는 닫힌 괄호인 arr[i]의 짝과 맞는지를 확인 후 맞지 않다면 false를 리턴하고 로직 전체를 종료
            if (braketsMap[lastElementOfStack] !== arr[i]) return false;
            
            // 짝이 맞다면 현재 stack의 가장 위에 위치한 괄호를 pop시켜서 stack에서 제거해줌
            stack.pop();
        }
    }

    // arr 배열전체를 돌면서 해당 로직을 이행한 후 stack에 어떠한 열린괄호라도 남아있다면 쌍이 맞지 않는 괄호들이 인풋으로 들어왔기 때문에 false를 반환, 그렇지 않고 stack이 비어져 있다면 모든 괄호쌍이 문제없이 유효한 괄호쌍이므로 true를 반환
    return stack.length ? false : true;
};