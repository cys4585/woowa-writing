# 1. **서론**

## **1.1. Multi Step Form을 개발한 프로젝트 배경 소개**

‘모우다’는 사람들이 속한 그룹 내에서 커피챗 등 가벼운 모임이나 취미 활동을 쉽게 조직하고 참여할 수 있도록 도와주는 서비스입니다. 이 프로젝트는 기존 업무용 커뮤니티 도구에서 취미 활동 및 가벼운 모임을 조직하는 데 어려움이 있다는 문제를 해결하기 위해 기획되었습니다. 모우다 서비스는 사용자가 자신이 속한 신뢰할 수 있는 집단에서 편하게 모임을 주선하고 참여할 수 있는 공간을 제공하여, 새로운 인연을 맺을 수 있도록 돕는 것을 목표로 합니다.

프로젝트 초기에는 빠른 개발을 위해 Single Step Form을 사용해 모임을 생성하고 참여하는 방식을 도입했지만, 사용자 경험을 개선하기 위해 Multi Step Form으로 전환했습니다. Multi Step Form을 통해 사용자에게 보다 직관적이고 부드러운 모임 생성 경험을 제공하고, 폼 작성을 단계별로 나눔으로써 인지 부하를 최소화하고자 했습니다.

## **1.2. Single Step Form과 Multi Step Form 비교**

### **1.2.1. Single Step Form**

**장점:**

1. **빠른 완료**: 모든 정보를 한 번에 입력할 수 있어, 단순한 입력의 경우 단시간에 폼 작성이 가능합니다.
2. **개발 및 유지보수 용이**: 구조가 단순하여 구현이 쉽고, 유지보수도 상대적으로 간단합니다.

**단점:**

1. **인지적 부담 증가**: 많은 정보가 한 페이지에 집중되기 때문에, 질문이 많거나 복잡할 경우 사용자가 부담을 느끼고 이탈할 가능성이 높습니다.
2. **모바일 친화성 부족**: 화면 크기가 작은 모바일 기기에서는 모든 정보를 한 번에 보여주는 것이 어려울 수 있습니다.
3. **조건부 질문의 비효율성**: 특정 질문이 사용자의 이전 답변에 따라 달라지는 경우, 이를 한 페이지에서 모두 관리하기 어렵습니다.

### **1.2.2. Multi Step Form**

**장점:**

1. **화면 공간 최적화**: 모바일 기기에서 각 단계별로 필요한 정보만 표시해 화면 복잡도를 줄일 수 있습니다.
2. **사용자 인지 부담 감소**: 정보를 단계별로 분할해 제공함으로써 사용자의 인지 부담을 줄일 수 있습니다.
3. **집중도 향상**: 사용자가 한 번에 하나의 작업에만 집중할 수 있어, 정확한 정보 입력을 유도할 수 있습니다.
4. **조건부 질문에 유리**: 이전 단계의 답변에 따라 다음 단계를 맞춤형으로 조정할 수 있어 유연한 폼 구성이 가능합니다.

**단점:**

1. **전체 프로세스의 길이 파악 어려움**: 사용자가 전체 폼의 길이를 한눈에 파악하기 어려워, 도중에 포기할 수 있습니다.
2. **복잡한 네비게이션**: 사용자가 이전 단계로 돌아가 정보를 수정하려 할 때 복잡한 네비게이션이 문제가 될 수 있습니다.
3. **컨텍스트 손실**: 이전 단계의 정보를 쉽게 참조할 수 없어 사용자가 헷갈릴 수 있습니다.
4. **구현 복잡성 증가**: 여러 단계를 관리해야 하기 때문에, 개발 및 유지보수가 상대적으로 더 복잡해질 수 있습니다.

---

# 2. **Multi Step Form 구현 시 주요 고려사항**

## **2.1. Step 관리 문제**

Multi Step Form을 구현할 때, 가장 중요한 문제는 각 단계를 관리하는 방식입니다. 사용자가 여러 단계에 걸쳐 데이터를 입력할 때, 각 단계를 어떻게 관리할지 결정하는 것이 중요합니다.

단계가 적절히 관리되지 않으면, 예를 들어 페이지 새로고침이나 뒤로/앞으로 가기 버튼을 눌렀을 때 사용자가 예상하지 못한 동작이 발생할 수 있습니다. URL을 통해 개별 스텝에 직접 접근하면, Form이 불완전하게 작성되거나 오류가 발생할 수 있습니다. 이 또한 사용자 경험에 큰 영향을 줄 수 있습니다.

## **2.2. 상태 유지 문제**

Multi Step Form을 구현할 때 또 다른 주요 문제는 상태 유지입니다. 사용자가 여러 단계를 거치며 데이터를 입력할 때, 이 상태를 일관되게 유지하는 것이 중요합니다. 그러나 웹 애플리케이션에서는 브라우저 의존으로 인한 문제가 있습니다. 브라우저로 페이지를 새로고침하거나 페이지를 이동하는 경우 상태가 손실될 위험이 있습니다.

## **2.3. UX 및 모바일 환경 최적화 문제**

UX를 위해 각 단계를 시각적으로 표시해 전체 프로세스와 현재 단계를 파악할 수 있어야 합니다. 사용자가 프로세스의 길이를 파악하지 못하는 경우, 도중에 포기할 우려가 있습니다.

모바일 환경에서 키보드로 인해 버튼이나 다른 입력 필드가 가려지는 등의 문제가 발생할 수 있습니다. 특히 iOS에서는 포커스 시 화면 확대 이슈가 발생할 수 있어 이를 고려한 처리가 필요합니다.

---

# 3. **Step 관리 문제 해결**

## 3.1. 다양한 접근 방식 검토

### 3.1.1. **useState를 이용한 스텝 관리**

```tsx
function MultiStepForm() {
  const [step, setStep] = useState("title");

  return (
    <>
      {step === "title" && <TitleStep />}
      {step === "place" && <PlaceStep />}
    </>
  );
}

function App() {
  return (
    <Routes>
      <Route path="/add-moim" element={<MultiStepForm />} />
    </Routes>
  );
}
```

폼의 각 스텝을 React의 `useState` 훅을 사용해 상태로 관리합니다. 폼 내에서 스텝을 이동할 때마다 상태 값을 업데이트하여 현재 스텝을 반영합니다.

- **장점**: 이 접근법은 간단하며, 컴포넌트 내에서 독립적으로 동작하므로 외부 의존성이 적습니다. 구현이 쉬워 빠르게 개발할 수 있습니다.
- **단점**: URL스텝 정보가 리액트 메모리 상에서 관리되므로, 페이지 리로드 시 현재 스텝을 유지할 수 없습니다. 또한, 브라우저의 히스토리 스택과 연동되지 않기 때문에 사용자가 뒤로 가기 버튼을 눌러도 이전 스텝으로 돌아갈 수 없습니다. 사용자가 브라우저 뒤로 가기를 할 경우 폼 프로세스가 중단될 위험이 있습니다.

### 3.1.2. **Path Parameter를 이용한 스텝 관리**

```tsx
function MultiStepForm() {
  const { step } = useParams();

  return (
    <>
      {step === "title" && <TitleStep />}
      {step === "place" && <PlaceStep />}
    </>
  );
}

function App() {
  return (
    <Routes>
      <Route path="/add-moim/:step" element={<MultiStepForm />} />
    </Routes>
  );
}
```

이 방식은 스텝을 URL의 path parameter로 관리합니다. 예를 들어, `https://mouda.site/add-moim/title`, `https://mouda.site/add-moim/place`와 같이 URL 경로에 스텝을 포함시킵니다.

- **장점**: 스텝 정보가 URL에 포함되기 때문에 페이지 리로드 시에도 현재 스텝이 유지됩니다.
- **단점**: 사용자가 직접 URL을 수정하여 스텝을 건너뛰거나 잘못된 순서로 접근할 위험이 있습니다. 특정 스텝을 독립적으로 접근할 수 없게 설계해야 하는데, path parameter를 이용하면 이 제약이 쉽게 무너질 수 있습니다.

### 3.1.3. **Query Parameter를 이용한 스텝 관리**

```tsx
function MultiStepForm() {
  const [searchParams] = useSearchParams();
  const step = searchParams.get("step");

  return (
    <>
      {step === "title" && <TitleStep />}
      {step === "place" && <PlaceStep />}
    </>
  );
}

function App() {
  return (
    <Routes>
      <Route path="/add-moim" element={<MultiStepForm />} />
    </Routes>
  );
}
```

스텝을 URL의 쿼리 파라미터로 관리하는 방식입니다. 예를 들어, `https://mouda.site/add-moim?step=title`, `https://mouda.site/add-moim?step=place`와 같이 URL에 `step`이라는 쿼리 파라미터를 추가합니다.

- **장점**: path parameter를 이용한 방식과 마찬가지로, URL에 스텝 정보가 포함되기 때문에 페이지 리로드 시에도 현재 스텝을 유지할 수 있습니다.
- **단점**: 사용자가 직접 query parameter를 변경하여 특정 스텝으로 이동할 수 있다는 위험이 있습니다. path parameter 방식과 마찬가지로 특정 스텝을 독립적으로 접근할 수 없다는 제약이 무너집니다.

### 3.1.4. **React Router의 state를 이용한 스텝 관리**

```tsx
function MultiStepForm() {
  const location = useLocation();
  const { step } = location.state || { step: "title" };

  return (
    <>
      {step === "title" && <TitleStep />}
      {step === "place" && <PlaceStep />}
    </>
  );
}

function App() {
  return (
    <Routes>
      <Route path="/add-moim" element={<MultiStepForm />} />
    </Routes>
  );
}
```

이 방법은 React Router의 `state`를 사용하여 스텝을 관리하는 방식입니다. history state 내에 저장되기 때문에, 페이지 전환 시 `state`에 현재 스텝 정보를 담아 다음 페이지로 전달할 수 있습니다.

- **장점**: 모든 스텝을 동일한 URL로 관리하면서도, 브라우저 히스토리 스택과의 연동이 가능합니다. 또한 라우팅 복잡성이 없고, URL에 스텝 정보가 노출되지 않으므로 외부 사용자가 스텝을 임의로 조작할 수 없습니다.
- **단점**: React Router의 `state`는 브라우저의 `history` 객체에 저장됩니다. 사용자가 브라우저의 개발자 도구를 통해 history를 조작해 state 정보가 유실될 수 있는 가능성이 있습니다.

### 3.1.5. 선택한 방식: React Router의 state를 이용

**선택 이유**:

- 개별 스텝을 URL로 직접 접근하지 못하게 하여 사용자 경험의 일관성을 유지하고 Form의 완결성을 보장합니다.
- 브라우저 히스토리 스택과 연동하여 관리할 수 있습니다. 페이지 리로드 및 뒤로/앞으로 가기 버튼으로 인해 사용자가 예상하지 못하게 폼이 중단되거나 잘못된 스텝에 접근할 가능성을 최소화합니다.

## 3.2. useFunnel 커스텀 훅 개발

### 3.2.1. useFunnel 훅의 목적과 기능

Multi Step Form에서 각 스텝을 효율적으로 관리하기 위해 `useFunnel` 훅을 설계했습니다. 복잡한 폼 관리 로직에서 스텝 관리 로직을 분리함으로써, 폼의 제어나 데이터 유효성 검사 등 핵심 비즈니스 로직에 집중할 수 있도록 합니다.

이 훅은 Multi Step Form에서 스텝 관리에 집중합니다. 현재 스텝이 무엇인지 추적하고, 스텝 이동을 처리하며, 각 스텝에 적절한 컴포넌트를 렌더링하는 역할을 맡습니다.

```tsx
import { ReactNode, useCallback } from "react";
import { useLocation, useNavigate } from "react-router-dom";

export default function useFunnel<Step extends string | number>(
  firstStep: Step
) {
  const location = useLocation(); // 현재 URL의 상태를 가져옴
  const navigate = useNavigate(); // 스텝 간 이동을 처리

  // 현재 스텝을 추적. firstStep을 초기값으로 설정
  const currentStep: Step = location.state?.step || firstStep;

  const goBack = () => {
    navigate(-1);
  };

  // 동일한 path로 navigate. state로 step을 관리
  const goNextStep = (nextStep: Step) => {
    navigate(location.pathname, {
      state: { step: nextStep },
    });
  };

  interface FunnelProps {
    step: Record<Step, ReactNode>;
  }

  // 현재 스텝에 맞는 컴포넌트를 렌더링
  const Funnel = useCallback(
    (props: FunnelProps) => {
      const { step } = props;
      return step[currentStep];
    },
    [currentStep]
  );

  return { currentStep, goBack, goNextStep, Funnel };
}
```

**주요 기능**:

- **현재 스텝 추적**: `useLocation`을 이용해 React Router의 `state`에서 현재 스텝 정보를 가져오며, 이 정보를 `currentStep` 변수로 관리합니다.
- **스텝 이동**: `goNextStep` 함수를 통해 다음 스텝으로 이동하고, `goBack` 함수를 통해 이전 스텝으로 돌아갑니다. 이 이동은 `useNavigate`를 통해 이루어집니다.
- **스텝 렌더링**: `Funnel` 컴포넌트를 사용하여, 현재 스텝에 해당하는 컴포넌트를 동적으로 렌더링합니다. `Funnel` 컴포넌트는 스텝별로 어떤 컴포넌트를 렌더링할지를 정의하는 객체를 받아, 현재 스텝에 맞는 컴포넌트를 화면에 표시합니다.

### 3.2.2. 사용 예시 및 이점

```tsx
export type MoimCreationStep =
  | "이름입력"
  | "장소선택"
  | "날짜/시간설정"
  | "최대인원설정"
  | "설명입력";

export default function MoimCreationPage() {
  const { Funnel, currentStep, goBack, goNextStep } =
    useFunnel<MoimCreationStep>("이름입력");

  const createMoim = (moimFormData: MoimFormData) => {
    // do something...
  };

  return (
    <Funnel
      step={{
        이름입력: <TitleStep onButtonClick={() => goNextStep("장소선택")} />,
        장소선택: (
          <PlaceStep onButtonClick={() => goNextStep("날짜/시간설정")} />
        ),
        "날짜/시간설정": (
          <DateAndTimeStep onButtonClick={() => goNextStep("최대인원설정")} />
        ),
        최대인원설정: (
          <MaxPeopleStep onButtonClick={() => goNextStep("설명입력")} />
        ),
        설명입력: (
          <DescriptionStep onButtonClick={() => createMoim(formData)} />
        ),
      }}
    />
  );
}
```

**이점**:

- **명확한 책임 분리**: 스텝 관리 로직은 `useFunnel`에게 맡기고, 컴포넌트는 폼 관리와 같은 핵심 비즈니스 로직에 집중할 수 있습니다.
- **재사용성**: `useFunnel` 훅은 특정 폼에 종속되지 않으며, 다양한 Multi Step Form에서 동일한 방식으로 스텝을 관리할 수 있습니다.

---

# 4. **상태 유지 문제 해결**

웹 애플리케이션에서 Multi Step Form을 구현할 때 상태 유지 또한 중요한 고려사항입니다.

## 4.1. 새로고침 시 상태 손실 문제

사용자가 여러 단계를 거치며 정보를 입력하는 도중, 브라우저를 새로고침 하는 경우 수집한 정보가 손실되지 않도록 조치해야 합니다. 새로고침 시 상태가 초기화되는 이유는 `useState`가 메모리에 저장되는 상태 값이기 때문입니다. 페이지가 새로고침되면 애플리케이션이 새로 렌더링되면서 상태도 초기화됩니다.

새로고침 시 상태가 손실되는 문제를 해결하기 위해 Web Storage API를 활용했습니다.

### 4.1.1. Web Storage API

Web Storage API는 브라우저에서 `키:값` 쌍을 직관적으로 저장할 수 있는 방법을 제공합니다. 이 저장소의 데이터는 도메인 단위로 접근이 제한됩니다. Web Storage는 세션 스토리지, 로컬 스토리지로 나뉩니다.

- 세션 스토리지는 임시 저장소로서, 탭 단위로 데이터를 저장하고 탭을 닫으면 데이터가 삭제됩니다.
- 로컬 스토리지는 영구 저장소로서, 탭을 닫거나 브라우저를 종료해도 데이터가 유지되고, 모든 탭과 창에서 공유됩니다.

### 4.1.2. 세션 스토리지를 활용한 문제 해결

입력 정보를 영구적으로 저장할 필요가 없는 경우, Multi Step Form을 통해 입력받은 정보를 세션 스토리지에 저장하여 새로고침 시 상태가 손실되는 문제를 해결할 수 있습니다.

아래 코드와 같은 방식으로 상태가 업데이트될 때 세션 스토리지를 동기화하여 상태 유실을 방지할 수 있습니다.

```tsx
const [formData, setFormData] = useState(() => {
  const item = sessionStorage.getItem("key");
  if (item !== null) {
    return JSON.parse(item);
  }
  return initialState;
});

useEffect(() => {
  sessionStorage.setItem("formData", formData);
}, [formData]);
```

위 방식은 구현이 간단합니다. 그러나 react state가 업데이트될 때마다 스토리지도 같이 업데이트된다는 낭비가 있습니다. 성능에 큰 문제를 일으키는 것은 아니지만, 스토리지 업데이트 빈도를 줄이기 위해 아래와 같이 구현했습니다.

```tsx
const [formData, setFormData] = useState(() => {
  const item = sessionStorage.getItem("key");
  if (item !== null) {
    return JSON.parse(item);
  }
  return 0;
});

// custom hook from 'react-router-dom';
useBeforeUnload(() => {
  sessionStorage.setItem("key", formData.toString());
});

useEffect(() => {
  sessionStorage.removeItem("key");
}, []);
```

위 코드는 beforeunload 이벤트를 활용한 방식입니다. 새로고침 직전 beforeunload 이벤트가 발생합니다. 이때 스토리지에 데이터를 임시로 저장했다가 다시 초기 렌더링이 되면 스토리지에서 데이터를 가져와 useState의 초기값으로 넣어줍니다. 이후 useEffect의 setup 함수를 활용해 스토리지를 비워줍니다. (beforeunload는 정확히 페이지를 이탈할 때 발생하는 이벤트입니다. 이와 관련한 추가 이슈를 4.3.1에서 다룹니다.)

## 4.2. useStatePersist 커스텀 훅 개발

### 4.2.1. useStatePersist 훅의 목적과 기능

각 스텝에서 입력받은 정보를 새로고침 시에도 유지할 수 있도록 스토리지로 관리하는 로직을 커스텀 훅 `useStatePersist`으로 분리했습니다. 상태 유지 로직을 추상화함으로써, 상태 관리 및 핵심 비즈니스 로직에 집중할 수 있도록 합니다. 또한 다양한 시나리오에서 상태 지속성을 요구하는 경우에 재사용 가능합니다.

```tsx
import { useCallback, useEffect, useState } from "react";
import { useBeforeUnload } from "react-router-dom";

interface UseStatePersistParams<StateType> {
  key: string;
  initialState: StateType | (() => StateType);
}

export default function useStatePersist<StateType>({
  key,
  initialState,
}: UseStatePersistParams<StateType>): [
  StateType,
  React.Dispatch<React.SetStateAction<StateType>>
] {
  // 세션 스토리지에서 지정된 key로 저장된 데이터를 가져옴
  // 만약 스토리지에 값이 있으면 JSON으로 파싱하여 반환하고, 없으면 initialState 값을 반환
  const getStoredValue = (): StateType => {
    try {
      const item = sessionStorage.getItem(key);
      if (item !== null) {
        return JSON.parse(item);
      }
    } catch (error) {
      console.error(`Error reading from session storage`, error);
    }

    return typeof initialState === "function"
      ? (initialState as () => StateType)()
      : initialState;
  };

  const setStoredValue = (value: StateType) => {
    try {
      sessionStorage.setItem(key, JSON.stringify(value));
    } catch (error) {
      console.error(`Error writing to session storage`, error);
    }
  };

  const removeStoredValue = useCallback(() => {
    try {
      sessionStorage.removeItem(key);
    } catch (error) {
      console.error(`Error removing item from  session storage`, error);
    }
  }, [key]);

  const [state, setState] = useState<StateType>(getStoredValue);

  // 페이지를 떠나거나 새로고침할 때, 상태를 세션 스토리지에 저장
  useBeforeUnload(() => {
    setStoredValue(state);
  });

  // 컴포넌트가 처음 렌더링된 후, 세션 스토리지에 저장된 값을 삭제
  useEffect(() => {
    removeStoredValue();
  }, [removeStoredValue]);

  return [state, setState];
}
```

**주요 기능:**

1. **상태 초기화 및 복원**: 훅이 처음 실행될 때, `sessionStorage`에 저장된 값이 있으면 이를 불러와서 초기 상태로 설정합니다. 만약 저장된 값이 없으면 전달된 `initialState`로 상태를 초기화합니다.
2. **상태 저장**: 페이지가 새로고침되거나 페이지를 이탈하기 전(`beforeunload` 이벤트 발생 시), 현재 상태를 `sessionStorage`에 저장합니다. 이를 통해 리액트 상태를 유지할 수 있습니다.
3. **스토리지 비우기**: 컴포넌트가 렌더링된 이후에는 세션 스토리지에 저장된 데이터를 제거하여, 해당 데이터를 다른 곳에서 접근할 수 없도록 합니다.

## 4.3. 브라우저 URL을 통한 페이지 이탈/접근 시 데이터 관리 문제

### 4.3.1. 문제1: URL 입력으로 페이지 이탈

beforeunload 이벤트 발생시 리액트 상태를 세션 스토리지에 저장하기 때문에, URL로 페이지를 이탈할 시 스토리지에 데이터가 저장되어 있습니다. 이로인해 Multi Step Form 페이지에 재접근시 이전에 입력해두었던 데이터가 초기값으로 세팅되었습니다. 이는 의도한 기능이 아닌 버그임으로 해결해야할 대상이었습니다. beforeunload 이벤트는 새로고침과 페이지 이탈을 구분할 수 없습니다. 이를 구분할 수 있는 Web API를 찾지 못했습니다.

해당 이슈를 해결하기 위해 리액트 상태를 유지하는 방법에 대해 다시 고민했습니다.

1. 상태 업데이트와 동시에 스토리지 동기화
   - 리액트 앱 내부 기능으로 페이지 이탈 시 → useEffect의 cleanup 함수로 스토리지를 비울 수 있습니다.
   - 브라우저 URL 입력으로 페이지 이탈 시 → beforeunload 이벤트 핸들러로 삭제하면 새로고침을 했을 때에도 삭제되는 문제가 남습니다.
2. beforeunload 이벤트 발생시 스토리지에 임시 저장, 렌더링시 스토리지로부터 상태 가져오기, useEffect setup 함수로 스토리지 비우기
   - 리액트 앱 내부 기능으로 페이지 이탈 시 → 스토리지에 데이터 저장이 되어있지 않은 상황이기 때문에 별도로 대응할 필요가 없습니다.
   - 브라우저 URL 입력으로 페이지 이탈 시 → beforeunload 이벤트 핸들러가 이미 스토리지에 데이터 저장을 위해 쓰이고 있기 때문에 상충됩니다.

페이지 이탈 시점에는 문제를 해결할 수 없었기 때문에, 차선책으로 페이지 최초 접근시에 `useStatePersist`를 호출하기 전 스토리지를 비우도록 했습니다. react router의 `useLocation(location.state.step)`과 `useNavigationType`으로 페이지 최초 접근을 감지했습니다.

```tsx
const isNewMoimCreation =
  currentStep === "이름입력" && navigationType === "PUSH";

if (isNewMoimCreation) {
  sessionStorage.removeItem("moimCreationInfo");
}
```

### 4.3.2. 문제2: URL 입력으로 페이지 접근

사용자가 부라우저 URL을 직접 입력하여 페이지에 접근한 경우, 기존의 react router의 API를 활용한 해결 방식으로는 페이지 최초 접근을 감지할 수 없었습니다.

이 문제를 해결하기 위해 Web API 중 Performance API를 활용했습니다. 브라우저의 navigationType으로 URL 기반 페이지 접근을 감지할 수 있었습니다. 기존의 페이지 최초 접근 판정 로직에 추가하여 URL 접근으로 인한 상태 초기화 문제를 해결했습니다.

```tsx
/**
 * @description 브라우저의 네비게이션 타입을 구분하는 함수
 * 링크 클릭, URL 직접 입력으로 페이지에 들어온 경우를 구분하기 위해 사용
 * react router로는 감지할 수 없어서 사용
 * ref: https://developer.mozilla.org/en-US/docs/Web/API/PerformanceNavigationTiming/type
 */
const getBrowserNavigationType = ():
  | "navigate"
  | "reload"
  | "back_forward"
  | "prerender"
  | undefined => {
  const navEntries = performance.getEntriesByType("navigation");
  if (navEntries.length > 0) {
    const navEntry = navEntries[0] as PerformanceNavigationTiming;
    return navEntry.type;
  }
};

export const isApprochedByUrl = () => {
  return getBrowserNavigationType() === "navigate";
};
```

```tsx
const isNewMoimCreation =
  currentStep === "이름입력" &&
  (navigationType === "PUSH" || isApprochedByUrl());

if (isNewMoimCreation) {
  sessionStorage.removeItem("moimCreationInfo");
}
```

---

# 5. **UX 개선 및 모바일 환경 최적화**

- **Step Indicator**:
  1. 사용자에게 전체 단계와 현재 단계를 알려주기 위해 Step Indicator UI를 개발하여 화면 하단부에 배치하였습니다.
  2. 기존 Step Indicator의 UI가 dot 형식으로 되어있어 사용자의 혼란(클릭으로 스텝 이동이 가능하다고 인지하는 사용자의 피드백)으로 인해 bar 형식으로 변경해 상단부로 이동하였습니다.
- **모바일 키보드 UI 대응**:

  - 모바일 환경에서 키보드 UI로 인해 하단 버튼이 가려지는 문제를 `visualViewport` API를 통해 해결했습니다. `innerHeight`와 `visualViewport.height`로 키보드 영역을 계산할 수 있습니다.

    - `innerHeight`는 전체 뷰포트 높이를 나타냅니다.
    - `visualViewport.height`는 실제로 보이는 화면 높이를 의미합니다.

    ```tsx
    const [keyboardHeight, setKeyboardHeight] = useState(0);

    useEffect(() => {
      const handleResize = () => {
        if (window.visualViewport) {
          const keyboardHeight =
            window.innerHeight - window.visualViewport.height;
          setKeyboardHeight(Math.max(0, keyboardHeight));
        }
      };

      window.visualViewport?.addEventListener("resize", handleResize);
      return () =>
        window.visualViewport?.removeEventListener("resize", handleResize);
    }, []);
    ```

- **크로스 브라우징 문제(iOS 환경 포커스 시 화면 확대) 해결**:
  - iOS에서 자동 포커스 시 화면이 확대되는 문제를 발견하고, 문제의 원인을 파악해 해결했습니다.
    - 원인: iOS/Safari에서는 input, select, textarea의 font-size가 16px보다 작은 경우, focus시 자동확대 됩니다.
    - 해결: input의 font-size를 16px로 높여 해결했습니다.
