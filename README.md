# WeCan Dockerized playbook for cc32d9's EOSIO Light-API

This template is provided for more agile and comfortable Ops-IT workflow of Light-API.
It's based fully on Light-API code with additions of docker containers prebuilt and provided by WeCan and automation for deployment developed by WeCan.

Docker images are available here:

```
https://hub.docker.com/r/wecandev/eosio-lightapi-wsapi
https://hub.docker.com/r/wecandev/eosio-lightapi-dbwriter
https://hub.docker.com/r/wecandev/eosio-lightapi-chronicle
```

We also provide snapshots for easier Light-API deployment https://backup.wecan.dev/wax/light_api/

# Usage

Include playbook:

```
- name: Import Light-api tasks with specific tags
  import_playbook: "./light-api/init-light_api.yml"
```

Include common operations tasks:

```
    head -n1 Makefile
    include ./light-api/Makefile
```

## Copyright and License for Light-API
All copyridght for EOSIO Light-API codebase belongs to cc32d9@gmail.com
https://github.com/cc32d9/eosio_light_api#copyright-and-license

We do not claim any rights to Light-API codebase.

## Copyright and License
MIT License

2024 WeCan.dev

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.