---
date: "2024-11-13T12:58:43+09:00"
draft: false
title: "ep4. frequency counter"
ShowToc: false
tags: ["알고리즘", "frequency counter"]
categories: ["DSA"]
---

## frequence counter

주말에 조금 쉬었더니 매일 공부하기로 했던 굳은 다짐이 느슨해지려고 한다. ㅠ 자, 다시 불태워보자.
알고리즘 문제를 해결하는 여러 가지 패턴 중에 frequency counter가 있다. 두 개의 배열이나 문자열을 새로운 {키: 값}으로 담고 해당 키나 값의 개수를 찾아 비교하는 방법이다. 예시로 애너그램(anagram: 동일한 단어의 순서를 바꾸어 다른 의미의 단어를 만드는 방법)을 확인하는 문제를 풀어봤다.

    function validAnagram(str1, str2) {
    if (str1.length !== str2.length) {
        return false;
    }

먼저 두 단어의 길이가 같지 않으면 애너그램 형식에 어긋나기 때문에 거짓이다.

    let counter1 = {}
    let counter2 = {}

각 단어의 알파벳 수를 확인해서 빈 객체{}에 담는다.

    for (let val of str1) {
        counter1[val] = (counter1[val] || 0) + 1;
    }
    for (let val of str2) {
        counter2[val] = (counter2[val] || 0) + 1;
    }

‘for ~ of’는 배열이나 문자열 등을 순회해서 값에 접근한다.
각 단어의 알파벳 개수를 확인해서 아직 할당되지 않았으면 최초로 1을 할당하고, 해당 알파벳 개수가 존재하면 1을 더한다. counter[val]에 값이 존재하지 않으면 undefined(거짓 값)이기 때문에 counter[val] || 0은 0이 된다.

    for (let key in counter1) {
        if (counter1[key] !== counter2[key])
            return false;
    }
    return true;

}

마지막으로 counter1 객체{}의 키를 순회했을 때 각 키의 개수가 counter2 객체{}의 키의 개수와 동일한지 확인해서, 맞으면 참, 다르면 거짓을 반환한다. 여기서 ‘for ~ in’은 객체{}의 프로퍼티를 순회해서 프로퍼티의 키에 접근한다.

Colt 강사님의 해답은 아래와 같다.
각 단어의 알파벳을 순회하는 부분은 내가 조금 수정해서 ‘for ~ of’ 형식으로 변경했다.
내가 풀이했던 방식과는 달리 알파벳의 개수를 담는 객체{}를 하나로 만들고, 두 번째 단어의 알파벳 개수와 비교하는 for 문을 만들면서 코드가 더 간결해졌다.

    function validAnagramColt(first, second) {
    		if (first.length !== second.length) {
    				return false;
    		}

    		const lookup = {}

    		for (let letter of first) {
    				// let letter = first[val];
    				lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1
    		}
    		for (let letter of second) {
    				// let letter = second[val]
    				if (!lookup[letter]) {
    						return false;
    				} else {
    						lookup[letter] -= 1
    				}
    		} return true
    }
