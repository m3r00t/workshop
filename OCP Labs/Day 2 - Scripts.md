HEXBOARD - https://github.com/2015-Middleware-Keynote/hexboard

1. Building a hexboard
# oc new-project demo

2. Setting environment
# export ACCESS_TOKEN=$(oc whoami -t)

3. Load template
# oc create -f https://raw.githubusercontent.com/2015-Middleware-Keynote/hexboard/master/app_template.json

4. Deploy sketch pod & hexboard
# oc new-app -l servicegroup=sketchpod openshift/nodejs-010-centos7~http://github.com/2015-Middleware-Keynote/sketchpod
# oc new-app -e "ACCESS_TOKEN=${ACCESS_TOKEN}" openshift/nodejs-010-centos7~http://github.com/2015-Middleware-Keynote/hexboard


5. Deploy the route
# oc expose svc/hexboard

6. Set admin access
# oc env dc/hexboard ADMIN_TOKEN="${ACCESS_TOKEN}"

Navigate to console: http://hexboard-demo.apps.imgv-ltd.co.uk/
(http://hexboard-demo.apps.imgv-ltd.co.uk/?admin=##########)


7. Scaling ()
# oc scale rc/sketchpod-1 --replicas=3

8. Healing 
# oc delete pod $(oc get pods | grep ^sketchpod | grep -v build | sed -e "s/^\(sketchpod-[0-9]*-[a-z0-9]*\)[ \t].*/\1 /" | head -n 5 | tr -d "\n" )



Set winner/hexboard size: 
# oc env dc/hexboard WINNER_COUNT=1
# oc env dc/hexboard HEXBOARD_SIZE=tiny

