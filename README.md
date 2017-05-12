# dockerautotest
# dockerautotest

This repo demonstrates how docker is building the same image 4 times when creating a pull request and merging it. The code is the one in the docker getting started + automated testing tutorials. 
When creating a pull request on branch testing:
it goes through steps 1-7 in the dockerfile, using cache. Then it goes again through steps 1-7, this time not using cache. Why doesn't it just build the tests, using cache??

    Building in Docker Cloud's infrastructure...
    Cloning into '.'...
    Warning: Permanently added the RSA host key for IP address '192.30.253.112' to the list of known hosts.
    Reset branch 'testing'
    Your branch is up-to-date with 'origin/testing'.
    Pulling cache layers for index.docker.io/incs/autotest:latest...
    Done!
    KernelVersion: 4.4.0-77-generic
    Arch: amd64
    BuildTime: 2017-03-28T19:26:53.326478373+00:00
    ApiVersion: 1.27
    Version: 17.03.1-ee-2
    MinAPIVersion: 1.12
    GitCommit: ad495cb
    Os: linux
    GoVersion: go1.7.5
    Starting build of index.docker.io/incs/autotest:latest...
    Step 1/7 : FROM python:2.7-slim
    ---> 1c7128a655f6
    Step 2/7 : WORKDIR /app
    ---> Using cache
    ---> 1582395e19e3
    Step 3/7 : COPY . /app
    ---> 9dfcea75a14e
    Removing intermediate container 2592fa1b0bd4
    Step 4/7 : RUN pip install -r requirements.txt
    ---> Running in 76d3a1a346f2
    Collecting Flask (from -r requirements.txt (line 1))
    Downloading Flask-0.12.1-py2.py3-none-any.whl (82kB)
    Collecting Redis (from -r requirements.txt (line 2))
    Downloading redis-2.10.5-py2.py3-none-any.whl (60kB)
    Collecting itsdangerous>=0.21 (from Flask->-r requirements.txt (line 1))
    Downloading itsdangerous-0.24.tar.gz (46kB)
    Collecting Jinja2>=2.4 (from Flask->-r requirements.txt (line 1))
    Downloading Jinja2-2.9.6-py2.py3-none-any.whl (340kB)
    Collecting Werkzeug>=0.7 (from Flask->-r requirements.txt (line 1))
    Downloading Werkzeug-0.12.1-py2.py3-none-any.whl (312kB)
    Collecting click>=2.0 (from Flask->-r requirements.txt (line 1))
    Downloading click-6.7-py2.py3-none-any.whl (71kB)
    Collecting MarkupSafe>=0.23 (from Jinja2>=2.4->Flask->-r requirements.txt (line 1))
    Downloading MarkupSafe-1.0.tar.gz
    Building wheels for collected packages: itsdangerous, MarkupSafe
    Running setup.py bdist_wheel for itsdangerous: started
    Running setup.py bdist_wheel for itsdangerous: finished with status 'done'
    Stored in directory: /root/.cache/pip/wheels/fc/a8/66/24d655233c757e178d45dea2de22a04c6d92766abfb741129a
    Running setup.py bdist_wheel for MarkupSafe: started
    Running setup.py bdist_wheel for MarkupSafe: finished with status 'done'
    Stored in directory: /root/.cache/pip/wheels/88/a7/30/e39a54a87bcbe25308fa3ca64e8ddc75d9b3e5afa21ee32d57
    Successfully built itsdangerous MarkupSafe
    Installing collected packages: itsdangerous, MarkupSafe, Jinja2, Werkzeug, click, Flask, Redis
    Successfully installed Flask-0.12.1 Jinja2-2.9.6 MarkupSafe-1.0 Redis-2.10.5 Werkzeug-0.12.1 click-6.7 itsdangerous-0.24
    ---> e74b83d2b9a9
    Removing intermediate container 76d3a1a346f2
    Step 5/7 : EXPOSE 80
    ---> Running in f2e1aec4d568
    ---> 542e0bca4edd
    Removing intermediate container f2e1aec4d568
    Step 6/7 : ENV NAME World
    ---> Running in ecae781b65a7
    ---> 535304993b57
    Removing intermediate container ecae781b65a7
    Step 7/7 : CMD python app.py
    ---> Running in d649be731d98
    ---> db9073e12db8
    Removing intermediate container d649be731d98
    Successfully built db9073e12db8
    Starting Test in docker-compose.test.yml...
    Building sut
    Step 1/7 : FROM python:2.7-slim
    ---> 1c7128a655f6
    Step 2/7 : WORKDIR /app
    ---> af338f8bd7b8
    Removing intermediate container b3102f5caa56
    Step 3/7 : COPY . /app
    ---> eafe3583b3a0
    Removing intermediate container dcf9a0bffab8
    Step 4/7 : RUN pip install -r requirements.txt
    ---> Running in 1fbe125fa97c
    Collecting Flask (from -r requirements.txt (line 1))
    Downloading Flask-0.12.1-py2.py3-none-any.whl (82kB)
    Collecting Redis (from -r requirements.txt (line 2))
    Downloading redis-2.10.5-py2.py3-none-any.whl (60kB)
    Collecting itsdangerous>=0.21 (from Flask->-r requirements.txt (line 1))
    Downloading itsdangerous-0.24.tar.gz (46kB)
    Collecting Jinja2>=2.4 (from Flask->-r requirements.txt (line 1))
    Downloading Jinja2-2.9.6-py2.py3-none-any.whl (340kB)
    Collecting Werkzeug>=0.7 (from Flask->-r requirements.txt (line 1))
    Downloading Werkzeug-0.12.1-py2.py3-none-any.whl (312kB)
    Collecting click>=2.0 (from Flask->-r requirements.txt (line 1))
    Downloading click-6.7-py2.py3-none-any.whl (71kB)
    Collecting MarkupSafe>=0.23 (from Jinja2>=2.4->Flask->-r requirements.txt (line 1))
    Downloading MarkupSafe-1.0.tar.gz
    Building wheels for collected packages: itsdangerous, MarkupSafe
    Running setup.py bdist_wheel for itsdangerous: started
    Running setup.py bdist_wheel for itsdangerous: finished with status 'done'
    Stored in directory: /root/.cache/pip/wheels/fc/a8/66/24d655233c757e178d45dea2de22a04c6d92766abfb741129a
    Running setup.py bdist_wheel for MarkupSafe: started
    Running setup.py bdist_wheel for MarkupSafe: finished with status 'done'
    Stored in directory: /root/.cache/pip/wheels/88/a7/30/e39a54a87bcbe25308fa3ca64e8ddc75d9b3e5afa21ee32d57
    Successfully built itsdangerous MarkupSafe
    Installing collected packages: itsdangerous, MarkupSafe, Jinja2, Werkzeug, click, Flask, Redis
    Successfully installed Flask-0.12.1 Jinja2-2.9.6 MarkupSafe-1.0 Redis-2.10.5 Werkzeug-0.12.1 click-6.7 itsdangerous-0.24
    ---> a6d4c599c48e
    Removing intermediate container 1fbe125fa97c
    Step 5/7 : EXPOSE 80
    ---> Running in 95556d4dc8e7
    ---> 00d404eb0708
    Removing intermediate container 95556d4dc8e7
    Step 6/7 : ENV NAME World
    ---> Running in 63df8695e07f
    ---> 7b5587714f98
    Removing intermediate container 63df8695e07f
    Step 7/7 : CMD python app.py
    ---> Running in 46194effc1ab
    ---> d3467a619739
    Removing intermediate container 46194effc1ab
    Successfully built d3467a619739
    Creating bcuqvpnspx5qz8tv8wyy2zy_sut_1
    hello
    Removing bcuqvpnspx5qz8tv8wyy2zy_sut_1 ...
    Removing bcuqvpnspx5qz8tv8wyy2zy_sut_1 ... done Going to remove bcuqvpnspx5qz8tv8wyy2zy_sut_1
    Tests in docker-compose.test.yml succeeded
    Pushing index.docker.io/incs/autotest:latest...
    Done!
    Build finished
    Build in 'testing' (9cd664f0) succeeded in 0:03:14
    
After merging in master, it again rebuilds everything using cache, and then rebuilds everything again, not using any cache. 

    Building in Docker Cloud's infrastructure...
    Cloning into '.'...
    Warning: Permanently added the RSA host key for IP address '192.30.253.113' to the list of known hosts.
    Switched to a new branch 'master'
    Pulling cache layers for index.docker.io/incs/autotest:latest...
    Done!
    KernelVersion: 4.4.0-77-generic
    Arch: amd64
    BuildTime: 2017-03-28T19:26:53.326478373+00:00
    ApiVersion: 1.27
    Version: 17.03.1-ee-2
    MinAPIVersion: 1.12
    GitCommit: ad495cb
    Os: linux
    GoVersion: go1.7.5
    Starting build of index.docker.io/incs/autotest:latest...
    Step 1/7 : FROM python:2.7-slim
    ---> 1c7128a655f6
    Step 2/7 : WORKDIR /app
    ---> Using cache
    ---> 1582395e19e3
    Step 3/7 : COPY . /app
    ---> d475302af781
    Removing intermediate container 5d53bf032a2d
    Step 4/7 : RUN pip install -r requirements.txt
    ---> Running in 518ba08d719e
    Collecting Flask (from -r requirements.txt (line 1))
    Downloading Flask-0.12.1-py2.py3-none-any.whl (82kB)
    Collecting Redis (from -r requirements.txt (line 2))
    Downloading redis-2.10.5-py2.py3-none-any.whl (60kB)
    Collecting itsdangerous>=0.21 (from Flask->-r requirements.txt (line 1))
    Downloading itsdangerous-0.24.tar.gz (46kB)
    Collecting Jinja2>=2.4 (from Flask->-r requirements.txt (line 1))
    Downloading Jinja2-2.9.6-py2.py3-none-any.whl (340kB)
    Collecting Werkzeug>=0.7 (from Flask->-r requirements.txt (line 1))
    Downloading Werkzeug-0.12.1-py2.py3-none-any.whl (312kB)
    Collecting click>=2.0 (from Flask->-r requirements.txt (line 1))
    Downloading click-6.7-py2.py3-none-any.whl (71kB)
    Collecting MarkupSafe>=0.23 (from Jinja2>=2.4->Flask->-r requirements.txt (line 1))
    Downloading MarkupSafe-1.0.tar.gz
    Building wheels for collected packages: itsdangerous, MarkupSafe
    Running setup.py bdist_wheel for itsdangerous: started
    Running setup.py bdist_wheel for itsdangerous: finished with status 'done'
    Stored in directory: /root/.cache/pip/wheels/fc/a8/66/24d655233c757e178d45dea2de22a04c6d92766abfb741129a
    Running setup.py bdist_wheel for MarkupSafe: started
    Running setup.py bdist_wheel for MarkupSafe: finished with status 'done'
    Stored in directory: /root/.cache/pip/wheels/88/a7/30/e39a54a87bcbe25308fa3ca64e8ddc75d9b3e5afa21ee32d57
    Successfully built itsdangerous MarkupSafe
    Installing collected packages: itsdangerous, MarkupSafe, Jinja2, Werkzeug, click, Flask, Redis
    Successfully installed Flask-0.12.1 Jinja2-2.9.6 MarkupSafe-1.0 Redis-2.10.5 Werkzeug-0.12.1 click-6.7 itsdangerous-0.24
    ---> a4cc3040d72a
    Removing intermediate container 518ba08d719e
    Step 5/7 : EXPOSE 80
    ---> Running in 32fc6cf65636
    ---> bf55f3d4aa48
    Removing intermediate container 32fc6cf65636
    Step 6/7 : ENV NAME World
    ---> Running in 614de00be1af
    ---> 95b94f42f67f
    Removing intermediate container 614de00be1af
    Step 7/7 : CMD python app.py
    ---> Running in d2ccc8f9e3f4
    ---> 904195e6ca9c
    Removing intermediate container d2ccc8f9e3f4
    Successfully built 904195e6ca9c
    Starting Test in docker-compose.test.yml...
    Building sut
    Step 1/7 : FROM python:2.7-slim
    ---> 1c7128a655f6
    Step 2/7 : WORKDIR /app
    ---> 5fff2669d589
    Removing intermediate container 3d2e4174ee73
    Step 3/7 : COPY . /app
    ---> 3ff823f162bb
    Removing intermediate container cd36796a6905
    Step 4/7 : RUN pip install -r requirements.txt
    ---> Running in 680afa9d4f31
    Collecting Flask (from -r requirements.txt (line 1))
    Downloading Flask-0.12.1-py2.py3-none-any.whl (82kB)
    Collecting Redis (from -r requirements.txt (line 2))
    Downloading redis-2.10.5-py2.py3-none-any.whl (60kB)
    Collecting itsdangerous>=0.21 (from Flask->-r requirements.txt (line 1))
    Downloading itsdangerous-0.24.tar.gz (46kB)
    Collecting Jinja2>=2.4 (from Flask->-r requirements.txt (line 1))
    Downloading Jinja2-2.9.6-py2.py3-none-any.whl (340kB)
    Collecting Werkzeug>=0.7 (from Flask->-r requirements.txt (line 1))
    Downloading Werkzeug-0.12.1-py2.py3-none-any.whl (312kB)
    Collecting click>=2.0 (from Flask->-r requirements.txt (line 1))
    Downloading click-6.7-py2.py3-none-any.whl (71kB)
    Collecting MarkupSafe>=0.23 (from Jinja2>=2.4->Flask->-r requirements.txt (line 1))
    Downloading MarkupSafe-1.0.tar.gz
    Building wheels for collected packages: itsdangerous, MarkupSafe
    Running setup.py bdist_wheel for itsdangerous: started
    Running setup.py bdist_wheel for itsdangerous: finished with status 'done'
    Stored in directory: /root/.cache/pip/wheels/fc/a8/66/24d655233c757e178d45dea2de22a04c6d92766abfb741129a
    Running setup.py bdist_wheel for MarkupSafe: started
    Running setup.py bdist_wheel for MarkupSafe: finished with status 'done'
    Stored in directory: /root/.cache/pip/wheels/88/a7/30/e39a54a87bcbe25308fa3ca64e8ddc75d9b3e5afa21ee32d57
    Successfully built itsdangerous MarkupSafe
    Installing collected packages: itsdangerous, MarkupSafe, Jinja2, Werkzeug, click, Flask, Redis
    Successfully installed Flask-0.12.1 Jinja2-2.9.6 MarkupSafe-1.0 Redis-2.10.5 Werkzeug-0.12.1 click-6.7 itsdangerous-0.24
    ---> 0f0ed4eb9df0
    Removing intermediate container 680afa9d4f31
    Step 5/7 : EXPOSE 80
    ---> Running in a6599f44d275
    ---> 49ef7a7b5d4b
    Removing intermediate container a6599f44d275
    Step 6/7 : ENV NAME World
    ---> Running in d99b89ed045f
    ---> bc383bceb0f7
    Removing intermediate container d99b89ed045f
    Step 7/7 : CMD python app.py
    ---> Running in 47586e076e32
    ---> 989c09b0b93d
    Removing intermediate container 47586e076e32
    Successfully built 989c09b0b93d
    Creating bhwfuvaajwe73ipttpgbmpf_sut_1
    hello
    Removing bhwfuvaajwe73ipttpgbmpf_sut_1 ...
    Removing bhwfuvaajwe73ipttpgbmpf_sut_1 ... done Going to remove bhwfuvaajwe73ipttpgbmpf_sut_1
    Tests in docker-compose.test.yml succeeded
    Pushing index.docker.io/incs/autotest:latest...
    Done!
    Build finished
    Build in 'master' (9cd664f0) succeeded in 0:02:32
