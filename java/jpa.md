
### 바인딩 변수 갯수 제한 32767개 (2 byte) 로 제한

```
userRepository.findByIdList(idList);  idList 의 32767개가 넘는 인자를 넘길 경우 오류 가 발생함.
```

- DataAccessResourceFailureException
- SQL Error: 0, SQLState: 08006
- java.io.IOException: Tried to send an out-of-range integer as a 2-byte value: 65536
