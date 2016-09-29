## Improvement

- Set a default rvm Ruby (2.3.0, currently)
- Allow certain environments to pass-through sudo invocations
  (namely, http\_proxy, https\_proxy, no\_proxy)

## Bug Fixes

- Always run the GOLANG and RubyGems setup scripts
  (Previously they would only execute for users who had
   specified an environment git repo)
