## Autogenerated clients
Several quircks exist for generating kube clients for activemq-artemis operator.

1) version of code-generator used to generate working clients is git commit f4fbdd3. later versions might generate faulty code due to operator-sdk version used.

2) as well as code-generator, one needs to clone kubernetes to $GOPATH/src/k8s.io/kubernetes as well as k8s.io/apimachinery. apimachinery version used is commit id 16cbbf9. 

3) Post-generation, 
    register.go needs to be edited to alter v2alpha1.AddToScheme and v2alpha2.AddToScheme calls. This calls should be replaced with apis.AddToScheme, apis being 	"github.com/artemiscloud/activemq-artemis-operator/pkg/apis"
    
    notions of ActiveMQArtemisAddressExpansion and ActiveMQArtemisScaledownExpansion need to be removed from respective clients.
 
 4) fake clients. Fake clients generated are faulty code, which was not fixed, but was left as a part of code-generator results. Do not use. 
 
 5) `./generate-groups.sh client github.com/artemiscloud/activemq-artemis-operator/pkg/client github.com/artemiscloud/activemq-artemis-operator/pkg/apis broker:v2alpha1,v2alpha2`
