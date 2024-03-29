# Alexander Lavrukhine

* **First Name**: Alexander
* **Last Name**: Lavrukhine
* **Email**: zanhesl@gmail.com
* **Phone number**: +79992054060
* **Web**: https://github.com/zanhesl

### Profile
Beginner junior developer seeking for improvement of personal front-end skills
with real-job practice and for gaining development experience.
Highly passionate towards JS development and software design
combined with intelligence to serve the needs of the business.

### Skills
**HTML 5, CSS3, JS, Photoshop** - advanced level

**Python and frameworks(Django, BeautifulSoup, NumPy, MatPlotLib)** - medium level

**C#, SQL, PHP, Azure** - beginner level

### Projects & Work Experience
Despite having rather insufficient working experience, I have done a few front-end
and python projects, which could be found on my personal Github page. It contains
both learning and developing ones.
### Code Example:
This is my small project for parsing balance of many Yandex.Money accounts on Python3:

```Python
import mechanize
import http.cookiejar
import requests
from bs4 import BeautifulSoup
import csv
from datetime import datetime
from multiprocessing import Pool
import time
from selenium import webdriver
from selenium.webdriver.common.keys import Keys


def get_html(br):
	r = br.response()
	data = r.read()
	return data

def get_page_data(html):
	soup = BeautifulSoup(html, 'lxml')
	balance = 'empty'
	try:
		balance = soup.find('span', class_='price__whole-amount text text_size_xxxxl text_view_primary text_weight_regular').text.strip()
	except Exception as e:
		print('No connection')

	return balance

def open_acc(login, password, number):
	# Browser
	br = mechanize.Browser()

	# Cookie Jar
	cj = http.cookiejar.LWPCookieJar()
	br.set_cookiejar(cj)

	# Browser options
	br.set_handle_equiv(True)
	br.set_handle_redirect(True)
	br.set_handle_referer(True)
	br.set_handle_robots(False)

	# Follows refresh 0 but not hangs on refresh > 0
	br.set_handle_refresh(mechanize._http.HTTPRefreshProcessor(), max_time=1)

	#br.set_debug_http(True)
	#br.set_debug_redirects(True)
	#br.set_debug_responses(True)

	# User-Agent
	br.addheaders = [('User-agent', 'Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.1) Gecko/2008071615 Fedora/3.0.1-1.fc9 Firefox/3.0.1')]

	br.open("https://passport.yandex.ru/auth?origin=money&retpath=https%3A%2F%2Fmoney.yandex.ru%2F%3Ffrom%3Dauth")
	br.select_form(nr=0)
	br['login'] = login
	br.select_form(nr=0)
	br['passwd'] = password
	br.submit()

	try:
		br.select_form(nr=0)
		br['answer'] = number
		br.submit()
	except Exception as es:
		pass



	return get_page_data(get_html(br))






def main():
	usernames = open('accounts_list.txt').read().split('\n')
	for user in usernames:
		user = user.split()
		print(open_acc(user[0], user[1], user[2]), ' rub ------', user[0])



if __name__ == '__main__':
	main()

```
### Education
Third-year ITMO student(ICT department), also took a number of front-end HTMLAcademy
courses on JavaScript and HTML&CSS.

I am currently studying English in my University on C2 level(passed C1 examination
successfully) and constantly trying to improve it by reading literature(both
professional and imaginative) and conversating with people.
