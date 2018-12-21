import requests
from bs4 import BeautifulSoup
from collections import OrderedDict
from itertools import count


def rednooby_cralwler(search_word, max_page):  #(search_word : 검색할 단어 / max_page : 찾을 최대 페이지수)
    url = 'https://search.naver.com/search.naver' # 네이버검색창 활용
    post_dict = OrderedDict()

    for page in count(1):
        params = {
            'query': search_word, # 입력하였던 단어
            'where': 'post',
            'start': (page - 1) * 10 + 1,
        }
        print(params)

        # 검색 단어로 검색 후 나온 url 저장
        response = requests.get(url, params=params)

        # 검색 된 url을 text형태로 저장
        html = response.text

        # 수업때 배운 인자로 BeuatifulSoup 지정
        soup = BeautifulSoup(html, 'html.parser')

        # 결과값 쪼개기
        title_list = soup.select('.sh_blog_title')

        for tag in title_list:
            if max_page and (page > max_page):  # 함수에서 입력한 max_page 그리고 max_page 보다 page가 클때
                return post_dict

            if tag['href'] in post_dict: # href라는 태크가 있으면 리턴
                return post_dict

            print(tag.text, tag['href'])
            post_dict[tag['href']] = tag.text

    return post_dict
