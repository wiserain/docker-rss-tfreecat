# docker-rss-tfree

클리앙 나스당의 시효니입니당 님이 만드신 rss parser를 담은 docker 이미지. 자세한 내용은 아래 출처를 참고바람.

> <https://www.clien.net/service/board/cm_nas/11498642> <https://www.clien.net/service/board/cm_nas/11269138>

## Usage

docker command:

```bash
docker run -d \
    --name=<container name> \
    --network=bridge \
    -p <local port you want>:8080 \
    wiserain/rss-tfree
```

docker-compose.yml:

```yaml
version: '2'

services:
  rss-tfree:
    image: wiserain/rss-tfree:latest
    container_name: <container name>
    restart: always
    network: bridge
    ports:
      - '<local port you want>:8080'
```

위의 방법 중 하나로 컨테이너를 생성한 뒤, 다음의 주소로 접속하면 된다.

```
http://localhost:port/rss/rss.rss?<key1>=<val1>&<key2>=<val2> ...
```

이 때 가능한 key, value 조합은 다음과 같다.

#### `cate=`

**필수항목** 다음의 카테고리 중 하나

- 영화, movie, tmovie
- 드라마, drama, tdrama
- 예능, 예능프로, 엔터, ent, tent
- tv프로, tv, 티비
- 애니,애니메이션,ani,tani
- 음악프로, 음악, music
- 유틸,util

#### `search=`

**필수항목** 원하는 검색어를 입력한다. 입력하지 않으면 해당 카테고리 첫 페이지 전체 목록을 출력한다.

#### `page=`

실제 웹사이트의 페이지에 대응하는 1보다 큰 정수. 생략할 경우 기본값은 1

### 예시

검색어 없이 영화 카테고리 3 페이지의 결과값을 검색하고 싶을 경우

```
http://localhost:port/rss/rss.rss?cate=영화&search=&page=3
```

드라마 "사랑의 온도" 1 페이지를 720p-NEXT로 검색할 경우

```
http://localhost:port/rss/rss.rss?cate=드라마&search=사랑의 온도 720p-next
```

윈도우 10을 검색할 경우

```
http://localhost:port/rss/rss.rss?cate=유틸&search=Windows10
```

드라마를 720p-NEXT로만 검색할 경우

```
http://localhost:port/rss/rss.rss?cate=드라마&search=720p-NEXT
```
