# Illumio API Package

## Description

Go package to easily interact with the Illumio API.

## Example Code
Nearly all functions that interact with your PCE are methods on the PCE type. For example, the code below prints all workloadss hostnames:
```
// Create PCE
pce := illumioapi.PCE{
   FQDN: "bep-lab.poc.segmentationpov.com",
   Port: 443,
   DisableTLSChecking: true}

// Login and ignore error checking for example
pce.Login("brian@email.com", "Password123")

// Get all workloads and ignore error checking for example
wklds, _, _ := pce.GetAllWorkloads()

// Iterate through workloads and print hostname
for _, w := range wklds {
    fmt.Println(w.Hostname)
}
```

## Tests and Examples ##
The `illumioapi_test` package includes some tests for the package. This can also be referenced for examples on how to use some of the functions.

## GoDoc Documentation ##
Full GoDoc Documentation (output of `godoc illumioapi` is avaialble in the main directory of the repo) and below.

```
PACKAGE DOCUMENTATION

package illumioapi
    import "/Users/brianpitta/go/src/github.com/brian1917/illumioapi/"


FUNCTIONS

func ProtocolList() map[int]string
    ProtocolList returns a map for the IANA protocol numbers.

TYPES

type APIKey struct {
    Href         string `json:"href,omitempty"`
    KeyID        string `json:"key_id,omitempty"`
    AuthUsername string `json:"auth_username,omitempty"`
    CreatedAt    string `json:"created_at,omitempty"`
    Name         string `json:"name,omitempty"`
    Description  string `json:"description,omitempty"`
    Secret       string `json:"secret,omitempty"`
}
    APIKey represents an API Key

type APIResponse struct {
    RespBody   string
    StatusCode int
    Header     http.Header
    Request    *http.Request
}
    APIResponse contains the information from the response of the API

type Actors struct {
    Actors     string      `json:"actors,omitempty"`
    Label      *Label      `json:"label,omitempty"`
    LabelGroup *LabelGroup `json:"label_group,omitempty"`
    Workload   *Workload   `json:"workload,omitempty"`
}
    Actors

type Agent struct {
    ActivePceFqdn string         `json:"active_pce_fqdn,omitempty"`
    Config        *Config        `json:"config,omitempty"`
    Href          string         `json:"href,omitempty"`
    SecureConnect *SecureConnect `json:"secure_connect,omitempty"`
    Status        *Status        `json:"status,omitempty"`
    TargetPceFqdn string         `json:"target_pce_fqdn,omitempty"`
}
    An Agent is an Agent on a Workload

func (a *Agent) GetID() string
    GetID returns the ID from the Href of an Agent

type AgentHealth struct {
    AuditEvent string `json:"audit_event,omitempty"`
    Severity   string `json:"severity,omitempty"`
    Type       string `json:"type,omitempty"`
}
    AgentHealth represents the Agent Health of the Status of a Workload

type AgentHealthErrors struct {
    Errors   []string `json:"errors,omitempty"`
    Warnings []string `json:"warnings,omitempty"`
}
    AgentHealthErrors represents the Agent Health Errors of the Status of a
    Workload This is depreciated - use AgentHealth

type Authentication struct {
    AuthToken string `json:"auth_token"`
}
    Authentication represents the response of the Authenticate API

type ChangeSubset struct {
    FirewallSettings      []*FirewallSettings      `json:"firewall_settings,omitempty"`
    IPLists               []*IPList                `json:"ip_lists,omitempty"`
    LabelGroups           []*LabelGroup            `json:"label_groups,omitempty"`
    RuleSets              []*RuleSets              `json:"rule_sets,omitempty"`
    SecureConnectGateways []*SecureConnectGateways `json:"secure_connect_gateways,omitempty"`
    Services              []*Services              `json:"services,omitempty"`
    VirtualServers        []*VirtualServers        `json:"virtual_servers,omitempty"`
    VirtualServices       []*VirtualServices       `json:"virtual_services,omitempty"`
}
    ChangeSubset Hash of pending hrefs, organized by model

type CompatibilityReport struct {
    LastUpdatedAt time.Time `json:"last_updated_at"`
    Results       Results   `json:"results"`
    QualifyStatus string    `json:"qualify_status"`
}
    CompatibilityReport is a compatibility report for a VEN in Idle status

type Config struct {
    LogTraffic               bool   `json:"log_traffic"`
    Mode                     string `json:"mode,omitempty"`
    SecurityPolicyUpdateMode string `json:"security_policy_update_mode,omitempty"`
    VisibilityLevel          string `json:"visibility_level,omitempty"`
}
    Config represents the Configuration of an Agent on a Workload

type Consumers struct {
    Actors         string          `json:"actors,omitempty"`
    IPList         *IPList         `json:"ip_list,omitempty"`
    Label          *Label          `json:"label,omitempty"`
    LabelGroup     *LabelGroup     `json:"label_group,omitempty"`
    VirtualService *VirtualService `json:"virtual_service,omitempty"`
    Workload       *Workload       `json:"workload,omitempty"`
}
    Consumers

type ConsumingSecurityPrincipals struct {
    Actors      []*Actors     `json:"actors"`
    Description string        `json:"description,omitempty"`
    Enabled     bool          `json:"enabled"`
    Href        string        `json:"href"`
    IPVersion   string        `json:"ip_version"`
    Statements  []*Statements `json:"statements"`
}
    ConsumingSecurityPrincipals

type CreatedBy struct {
    Href string `json:"href"`
}
    CreatedBy represents the CreatedBy property of an object

type DeletedBy struct {
    Href string `json:"href,omitempty"`
}
    DeletedBy represents the Deleted By property of an object

type Destinations struct {
    Include [][]Include `json:"include"`
    Exclude []Exclude   `json:"exclude"`
}
    Destinations represents the destination query portion of the explorer
    API

type Dst struct {
    IP       string    `json:"ip"`
    Workload *Workload `json:"workload,omitempty"`
}
    Dst is the provider workload details

type Exclude struct {
    Label          *Label     `json:"label,omitempty"`
    Workload       *Workload  `json:"workload,omitempty"`
    IPAddress      *IPAddress `json:"ip_address,omitempty"`
    Port           int        `json:"port,omitempty"`
    ToPort         int        `json:"to_port,omitempty"`
    Proto          int        `json:"proto,omitempty"`
    Process        string     `json:"process_name,omitempty"`
    WindowsService string     `json:"windows_service_name,omitempty"`
}
    Exclude represents the type of objects used in an include query. The
    exclude struct should only have the following combinations: label only,
    workload only, IP address only, Port and/or protocol only. Example -
    Label and Workload cannot both be non-nil Example - Port and Proto can
    both be non-nil (e.g., port 3306 and proto 6)

type ExpSrv struct {
    Port           int    `json:"port,omitempty"`
    Proto          int    `json:"proto,omitempty"`
    Process        string `json:"process_name,omitempty"`
    WindowsService string `json:"windows_service_name,omitempty"`
}
    ExpSrv is a service in the explorer response

type ExplorerServices struct {
    Include []Include `json:"include"`
    Exclude []Exclude `json:"exclude"`
}
    ExplorerServices represent services to be included or excluded in the
    explorer query

type FirewallSettings struct {
    Href string `json:"href"`
}
    FirewallSettings

type FlowUploadResp struct {
    NumFlowsReceived int       `json:"num_flows_received"`
    NumFlowsFailed   int       `json:"num_flows_failed"`
    FailedFlows      []*string `json:"failed_flows,omitempty"`
}
    FlowUploadResp is the response from the traffic upload API

type IPAddress struct {
    Value string `json:"value,omitempty"`
}
    IPAddress represents an IP Address

type IPList struct {
    CreatedAt             string     `json:"created_at,omitempty"`
    CreatedBy             *CreatedBy `json:"created_by,omitempty"`
    DeletedAt             string     `json:"deleted_at,omitempty"`
    DeletedBy             *DeletedBy `json:"deleted_by,omitempty"`
    Description           string     `json:"description,omitempty"`
    ExternalDataReference string     `json:"external_data_reference,omitempty"`
    ExternalDataSet       string     `json:"external_data_set,omitempty"`
    Href                  string     `json:"href,omitempty"`
    IPRanges              []*IPRange `json:"ip_ranges,omitempty"`
    Name                  string     `json:"name,omitempty"`
    UpdatedAt             string     `json:"updated_at,omitempty"`
    UpdatedBy             *UpdatedBy `json:"updated_by,omitempty"`
}
    IPList represents an IP List in the Illumio PCE.

type IPRange struct {
    Description string `json:"description,omitempty"`
    Exclusion   bool   `json:"exclusion,omitempty"`
    FromIP      string `json:"from_ip,omitempty"`
    ToIP        string `json:"to_ip,omitempty"`
}
    IPRange repsents one of the IP ranges of an IP List.

type IPTablesRules struct {
    Actors      []*Actors     `json:"actors"`
    Description string        `json:"description,omitempty"`
    Enabled     bool          `json:"enabled"`
    Href        string        `json:"href"`
    IpVersion   string        `json:"ip_version"`
    Statements  []*Statements `json:"statements"`
}
    IpTablesRules

type Include struct {
    Label          *Label     `json:"label,omitempty"`
    Workload       *Workload  `json:"workload,omitempty"`
    IPAddress      *IPAddress `json:"ip_address,omitempty"`
    Port           int        `json:"port,omitempty"`
    ToPort         int        `json:"to_port,omitempty"`
    Proto          int        `json:"proto,omitempty"`
    Process        string     `json:"process_name,omitempty"`
    WindowsService string     `json:"windows_service_name,omitempty"`
}
    Include represents the type of objects used in an include query. The
    include struct should be label only, workload only, IP address only,
    Port and/or protocol only. Example - Label and Workload cannot both be
    non-nil Example - Port and Proto can both be non-nil (e.g., port 3306
    and proto 6)

type IngressServices struct {
}
    IngressServices

type Interface struct {
    Address               string `json:"address,omitempty"`
    CidrBlock             *int   `json:"cidr_block,omitempty"`
    DefaultGatewayAddress string `json:"default_gateway_address,omitempty"`
    FriendlyName          string `json:"friendly_name,omitempty"`
    LinkState             string `json:"link_state,omitempty"`
    Name                  string `json:"name,omitempty"`
}
    An Interface represent the Interfaces of a Workload

type Label struct {
    CreatedAt             string     `json:"created_at,omitempty"`
    CreatedBy             *CreatedBy `json:"created_by,omitempty"`
    Deleted               bool       `json:"deleted,omitempty"`
    ExternalDataReference string     `json:"external_data_reference,omitempty"`
    ExternalDataSet       string     `json:"external_data_set,omitempty"`
    Href                  string     `json:"href,omitempty"`
    Key                   string     `json:"key,omitempty"`
    UpdatedAt             string     `json:"updated_at,omitempty"`
    UpdatedBy             *UpdatedBy `json:"updated_by,omitempty"`
    Value                 string     `json:"value,omitempty"`
}
    A Label represents an Illumio Label.

type LabelGroup struct {
    Description           string       `json:"description,omitempty"`
    ExternalDataReference string       `json:"external_data_reference,omitempty"`
    ExternalDataSet       string       `json:"external_data_set,omitempty"`
    Href                  string       `json:"href,omitempty"`
    Key                   string       `json:"key,omitempty"`
    Labels                []*Label     `json:"labels,omitempty"`
    Name                  string       `json:"name,omitempty"`
    SubGroups             []*SubGroups `json:"sub_groups,omitempty"`
    Usage                 *Usage       `json:"usage,omitempty"`
}
    LabelGroup represents a Label Group in the Illumio PCE

type OpenServicePorts struct {
    Address        string `json:"address,omitempty"`
    Package        string `json:"package,omitempty"`
    Port           int    `json:"port,omitempty"`
    ProcessName    string `json:"process_name,omitempty"`
    Protocol       int    `json:"protocol,omitempty"`
    User           string `json:"user,omitempty"`
    WinServiceName string `json:"win_service_name,omitempty"`
}
    OpenServicePorts represents open ports for a service running on a
    workload

type Org struct {
    Href        string `json:"href"`
    DisplayName string `json:"display_name"`
    ID          int    `json:"org_id"`
}
    Org is an an organization in a SaaS PCE

type PCE struct {
    FQDN               string
    Port               int
    Org                int
    User               string
    Key                string
    DisableTLSChecking bool
    LabelMapH          map[string]Label
    LabelMapKV         map[string]Label
}
    PCE represents an Illumio PCE and the necessary info to authenticate

func (p *PCE) BulkWorkload(workloads []Workload, method string) ([]APIResponse, error)
    BulkWorkload takes a bulk action on an array of workloads. Method must
    be create, update, or delete

func (p *PCE) CreateBoundService(virtualService VirtualService) (VirtualService, APIResponse, error)
    CreateBoundService creates a new Virtual service in the Illumio PCE.

func (p *PCE) CreateIPList(ipList IPList) (IPList, APIResponse, error)
    CreateIPList creates a new IP List in the Illumio PCE.

    The function will not remove properties not in the POST schema (e.g.,
    CreatedAt)

func (p *PCE) CreateLabel(label Label) (Label, APIResponse, error)
    CreateLabel creates a new Label in the Illumio PCE.

func (p *PCE) CreatePairingKey(pairingProfile PairingProfile) (APIResponse, error)
    CreatePairingKey creates a pairing key from a pairing profile.

func (p *PCE) CreatePairingProfile(pairingProfile PairingProfile) (APIResponse, error)
    CreatePairingProfile creates a new pairing profile in the Illumio PCE.

func (p *PCE) CreateService(service Service) (Service, APIResponse, error)
    CreateService creates a new service in the Illumio PCE

func (p *PCE) CreateWorkload(workload Workload) (Workload, APIResponse, error)
    CreateWorkload creates a new unmanaged workload in the Illumio PCE

func (p *PCE) DeleteHref(href string) (APIResponse, error)
    DeleteHref deletes an existing object in the PCE based on its href.

func (p *PCE) GetAllAPIKeys(userHref string) ([]APIKey, APIResponse, error)
    GetAllAPIKeys gets all the APIKeys associated with a user

func (p *PCE) GetAllActiveIPLists() ([]IPList, APIResponse, error)
    GetAllActiveIPLists returns a slice of draft IPLists If there are more
    than 500 IP Lists, async will run.

func (p *PCE) GetAllDraftIPLists() ([]IPList, APIResponse, error)
    GetAllDraftIPLists returns a slice of draft IPLists If there are more
    than 500 IP Lists, async will run.

func (p *PCE) GetAllIPLists() ([]IPList, []APIResponse, error)
    GetAllIPLists returns a slice of all IPLists in the PCE. The function
    combines the query to get draft and active IP Lists. If there are more
    than 500 of either, async queries will run. The []APIResponse will have
    two entries - first is for draft, second for active. The HREF will
    indicate if it's active or draft.

func (p *PCE) GetAllLabelGroups(provisionStatus string) ([]LabelGroup, APIResponse, error)
    GetAllLabelGroups returns a slice of all Label Groups of a specific
    provision status in the Illumio PCE.

    The pvoision status must be "draft" or "active". The first call does not
    use the async option. If the response array length is >=500, it is
    re-run enabling async.

func (p *PCE) GetAllLabels() ([]Label, APIResponse, error)
    GetAllLabels returns a slice of all Labels in the Illumio PCE. The first
    API call to the PCE does not use the async option. If the array length
    is >=500, it re-runs with async.

func (p *PCE) GetAllPairingProfiles() ([]PairingProfile, APIResponse, error)
    GetAllPairingProfiles gets all pairing profiles in the Illumio PCE.

func (p *PCE) GetAllRuleSets(provisionStatus string) ([]RuleSet, APIResponse, error)
    GetAllRuleSets returns a slice of Rulesets for all RuleSets in the
    Illumio PCE

func (p *PCE) GetAllServices(provisionStatus string) ([]Service, APIResponse, error)
    GetAllServices returns a slice of Services for each Service in the
    Illumio PCE. provisionStatus must either be "draft" or "active". The
    first API call to the PCE does not use the async option. If the array
    length is >=500, it re-runs with async.

func (p *PCE) GetAllVirtualServices(provisionStatus string) ([]VirtualService, APIResponse, error)
    GetAllVirtualServices returns a slice of all Virtual services of a
    specific provision status in the Illumio PCE.

    The pvoision status must be "draft" or "active". The first call does not
    use the async option. If the response array length is >=500, it is
    re-run enabling async.

func (p *PCE) GetAllVulnReports() ([]VulnerabilityReport, APIResponse, error)
    GetAllVulnReports returns a slice of all Vulnerability Reports in the
    Illumio PCE. The first call does not use the async option. If the
    response slice length is >=500, it is re-run enabling async.

func (p *PCE) GetAllVulns() ([]Vulnerability, APIResponse, error)
    GetAllVulns returns a slice of all Vulnerabilities in the Illumio PCE.
    The first call does not use the async option. If the response slice
    length is >=500, it is re-run enabling async.

func (p *PCE) GetAllWorkloads() ([]Workload, APIResponse, error)
    GetAllWorkloads returns an slice of workloads in the Illumio PCE. The
    first API call to the PCE does not use the async option. If the array
    length is >=500, it re-runs with async.

func (p *PCE) GetCompatibilityReport(w Workload) (CompatibilityReport, APIResponse, error)
    GetCompatibilityReport returns the compatibility report for a VEN

func (p *PCE) GetIPList(name string) (IPList, APIResponse, error)
    GetIPList queries returns the IP List based on name. Provisioned IP
    lists checked before draft

func (p *PCE) GetLabelMaps() (APIResponse, error)
    GetLabelMaps returns a map of labels with the HREF as the key

func (p *PCE) GetLabelbyHref(href string) (Label, APIResponse, error)
    GetLabelbyHref returns a label based on the provided HREF.

func (p *PCE) GetLabelbyKeyValue(key, value string) (Label, APIResponse, error)
    GetLabelbyKeyValue finds a label based on the key and value. It will
    only return one Label that is an exact match.

func (p *PCE) GetTrafficAnalysis(query TrafficQuery) ([]TrafficAnalysis, APIResponse, error)
    GetTrafficAnalysis gets flow data from Explorer.

func (p *PCE) GetVersion() (Version, error)
    GetVersion returns the version of the PCE

func (p *PCE) GetWkldByHref(href string) (Workload, APIResponse, error)
    GetWkldByHref returns the workload with a specific href

func (p *PCE) GetWkldHostMap() (map[string]Workload, APIResponse, error)
    GetWkldHostMap returns a map of all workloads with the hostname as the
    key.

func (p *PCE) GetWkldHrefMap() (map[string]Workload, APIResponse, error)
    GetWkldHrefMap returns a map of all workloads with the Href as the key.

func (p *PCE) IterateTrafficJString(stdout bool) (string, error)
    IterateTrafficJString iterates over each workload in a PCE to get all
    traffic data

func (p *PCE) Login(user, password string) (UserLogin, []APIResponse, error)
    Login authenticates to the PCE. Login will populate the User, Key, and
    Org fields in the PCE instance. Login will use a temporary session token
    that expires after 10 minutes.

func (p *PCE) LoginAPIKey(user, password, name, desc string) (UserLogin, []APIResponse, error)
    LoginAPIKey authenticates to the PCE. Login will populate the User, Key,
    and Org fields in the PCE instance. LoginAPIKey will create a permanent
    API Key with the provided name and description fields.

func (p *PCE) ProvisionHref(href string) (APIResponse, error)
    ProvisionHref only works with IPlists right now - needs to be updated

func (p *PCE) UpdateBoundService(virtualService VirtualService) (APIResponse, error)
    UpdateBoundService updates an existing Virtual service in the Illumio
    PCE.

    The provided BoundService struct must include an Href. Properties that
    cannot be included in the PUT method will be ignored.

func (p *PCE) UpdateIPList(iplist IPList) (APIResponse, error)
    UpdateIPList updates an existing IP List in the Illumio PCE.

    The provided IPList struct must include an Href. The function will
    remove properties not included in the PUT schema.

func (p *PCE) UpdateLabel(label Label) (APIResponse, error)
    UpdateLabel updates an existing label in the Illumio PCE. The provided
    label struct must include an Href. Properties that cannot be included in
    the PUT method will be ignored.

func (p *PCE) UpdateService(service Service) (APIResponse, error)
    UpdateService updates an existing service object in the Illumio PCE

func (p *PCE) UpdateWorkload(workload Workload) (APIResponse, error)
    UpdateWorkload updates an existing workload in the Illumio PCE The
    provided workload struct must include an Href. Properties that cannot be
    included in the PUT method will be ignored.

func (p *PCE) UploadTraffic(filename string, headerLine bool) (UploadFlowResults, error)
    UploadTraffic uploads a csv to the PCE with traffic flows. filename
    should be the path to a csv file with 4 cols: src_ip, dst_ip, port,
    protocol (IANA numerical format 6=TCP, 17=UDP) When headerLine = true,
    the first line of the CSV is skipped. If there are more than 999 entries
    in the CSV, it creates chunks of 999

func (p *PCE) WorkloadUpgrade(wkldHref, targetVersion string) (APIResponse, error)
    WorkloadUpgrade upgrades the VEN version on the workload

type PairingKey struct {
    ActivationCode string `json:"activation_code,omitempty"`
}
    PairingKey represents a VEN pairing key

type PairingProfile struct {
    AllowedUsesPerKey     string     `json:"allowed_uses_per_key,omitempty"`
    AppLabelLock          bool       `json:"app_label_lock"`
    CreatedAt             string     `json:"created_at,omitempty"`
    CreatedBy             *CreatedBy `json:"created_by,omitempty"`
    Description           string     `json:"description,omitempty"`
    Enabled               bool       `json:"enabled"`
    EnvLabelLock          bool       `json:"env_label_lock"`
    ExternalDataReference string     `json:"external_data_reference,omitempty"`
    ExternalDataSet       string     `json:"external_data_set,omitempty"`
    Href                  string     `json:"href,omitempty,omitempty"`
    IsDefault             bool       `json:"is_default,omitempty"`
    KeyLifespan           string     `json:"key_lifespan,omitempty"`
    Labels                []*Label   `json:"labels,omitempty"`
    LastPairingAt         string     `json:"last_pairing_at,omitempty"`
    LocLabelLock          bool       `json:"loc_label_lock"`
    LogTraffic            bool       `json:"log_traffic"`
    LogTrafficLock        bool       `json:"log_traffic_lock"`
    Mode                  string     `json:"mode,omitempty"`
    ModeLock              bool       `json:"mode_lock"`
    Name                  string     `json:"name,omitempty"`
    RoleLabelLock         bool       `json:"role_label_lock"`
    TotalUseCount         int        `json:"total_use_count,omitempty"`
    UpdatedAt             string     `json:"updated_at,omitempty"`
    UpdatedBy             *UpdatedBy `json:"updated_by,omitempty,omitempty"`
    VisibilityLevel       string     `json:"visibility_level,omitempty"`
    VisibilityLevelLock   bool       `json:"visibility_level_lock"`
}
    PairingProfile represents a pairing profile in the Illumio PCE

type PortProtos struct {
    Include []Include `json:"include"`
    Exclude []Exclude `json:"exclude"`
}
    PortProtos represents the ports and protocols query portion of the
    exporer API

type ProductVersion struct {
    Build           int    `json:"build,omitempty"`
    EngineeringInfo string `json:"engineering_info,omitempty"`
    LongDisplay     string `json:"long_display,omitempty"`
    ReleaseInfo     string `json:"release_info,omitempty"`
    ShortDisplay    string `json:"short_display,omitempty"`
    Version         string `json:"version,omitempty"`
}
    ProductVersion represents the version of the product

type Providers struct {
    Actors         string          `json:"actors,omitempty"`
    IPList         *IPList         `json:"ip_list,omitempty"`
    Label          *Label          `json:"label,omitempty"`
    LabelGroup     *LabelGroup     `json:"label_group,omitempty"`
    VirtualServer  *VirtualServer  `json:"virtual_server,omitempty"`
    VirtualService *VirtualService `json:"virtual_service,omitempty"`
    Workload       *Workload       `json:"workload,omitempty"`
}
    Providers

type Provision struct {
    ChangeSubset      *ChangeSubset `json:"change_subset,omitempty"`
    UpdateDescription string        `json:"update_description,omitempty"`
}
    Provision

type QualifyTest struct {
    RequiredPackages          []string `json:"required_packages"`
    RequiredPackagesInstalled bool     `json:"required_packages_installed"`
    Status                    string   `json:"status"`
    RequiredPackagesMissing   []string `json:"required_packages_missing"`
    Ipv4ForwardingEnabled     string   `json:"ipv4_forwarding_enabled"`
    Ipv4ForwardingPktCnt      int      `json:"ipv4_forwarding_pkt_cnt"`
    IptablesRuleCnt           int      `json:"iptables_rule_cnt"`
    Ipv6GlobalScope           string   `json:"ipv6_global_scope"`
    Ipv6ActiveConnCnt         int      `json:"ipv6_active_conn_cnt"`
    IP6TablesRuleCnt          int      `json:"ip6tables_rule_cnt"`
}
    QualifyTest is part of compatibility report

type ResolveLabelsAs struct {
    Consumers []string `json:"consumers"`
    Providers []string `json:"providers"`
}
    ResolveLabelsAs

type Results struct {
    QualifyTests []QualifyTest `json:"qualify_tests"`
}
    Results are the list of qualify tests

type Rule struct {
    Consumers                   []*Consumers                 `json:"consumers"`
    ConsumingSecurityPrincipals *ConsumingSecurityPrincipals `json:"consuming_security_principals,omitempty"`
    Description                 string                       `json:"description,omitempty"`
    Enabled                     bool                         `json:"enabled"`
    ExternalDataReference       interface{}                  `json:"external_data_reference,omitempty"`
    ExternalDataSet             interface{}                  `json:"external_data_set,omitempty"`
    Href                        string                       `json:"href,omitempty"`
    IngressServices             []*IngressServices           `json:"ingress_services"`
    Providers                   []*Providers                 `json:"providers"`
    ResolveLabelsAs             *ResolveLabelsAs             `json:"resolve_labels_as"`
    SecConnect                  bool                         `json:"sec_connect,omitempty"`
    UnscopedConsumers           bool                         `json:"unscoped_consumers,omitempty"`
    UpdateType                  string                       `json:"update_type,omitempty"`
}
    Rules

type RuleSet struct {
    CreatedAt             string           `json:"created_at"`
    CreatedBy             *CreatedBy       `json:"created_by,omitempty"`
    DeletedAt             string           `json:"deleted_at"`
    DeletedBy             *DeletedBy       `json:"deleted_by,omitempty"`
    Description           string           `json:"description"`
    Enabled               bool             `json:"enabled"`
    ExternalDataReference interface{}      `json:"external_data_reference,omitempty"`
    ExternalDataSet       interface{}      `json:"external_data_set,omitempty"`
    Href                  string           `json:"href,omitempty"`
    IPTablesRules         []*IPTablesRules `json:"ip_tables_rules,omitempty"`
    Name                  string           `json:"name"`
    Rules                 []*Rule          `json:"rules"`
    Scopes                [][]*Scopes      `json:"scopes"`
    UpdateType            string           `json:"update_type,omitempty"`
    UpdatedAt             string           `json:"updated_at"`
    UpdatedBy             *UpdatedBy       `json:"updated_by,omitempty"`
}
    Ruleset

type RuleSets struct {
    Href string `json:"href"`
}
    RuleSets

type Scopes struct {
    Label      *Label      `json:"label,omitempty"`
    LabelGroup *LabelGroup `json:"label_group,omitempty"`
}
    Scope

type SecureConnect struct {
    MatchingIssuerName string `json:"matching_issuer_name,omitempty"`
}
    SecureConnect represents SecureConnect for an Agent on a Workload

type SecureConnectGateways struct {
    Href string `json:"href"`
}
    SecureConnectGateways

type Service struct {
    CreatedAt             string            `json:"created_at,omitempty"`
    CreatedBy             *CreatedBy        `json:"created_by,omitempty"`
    DeletedAt             string            `json:"deleted_at,omitempty"`
    DeletedBy             *DeletedBy        `json:"deleted_by,omitempty"`
    Description           string            `json:"description,omitempty"`
    DescriptionURL        string            `json:"description_url,omitempty"`
    ExternalDataReference string            `json:"external_data_reference,omitempty"`
    ExternalDataSet       string            `json:"external_data_set,omitempty"`
    Href                  string            `json:"href,omitempty"`
    Name                  string            `json:"name"`
    ProcessName           string            `json:"process_name,omitempty"`
    ServicePorts          []*ServicePort    `json:"service_ports,omitempty"`
    UpdateType            string            `json:"update_type,omitempty"`
    UpdatedAt             string            `json:"updated_at,omitempty"`
    UpdatedBy             *UpdatedBy        `json:"updated_by,omitempty"`
    WindowsServices       []*WindowsService `json:"windows_services,omitempty"`
}
    Service represent a service in the Illumio PCE

type ServiceBinding struct {
}
    A ServiceBinding represents a Service Binding in the Illumio PCE

type ServicePort struct {
    IcmpCode int `json:"icmp_code,omitempty"`
    IcmpType int `json:"icmp_type,omitempty"`
    ID       int `json:"id,omitempty"`
    Port     int `json:"port,omitempty"`
    Protocol int `json:"protocol"`
    ToPort   int `json:"to_port,omitempty"`
}
    ServicePort represent port and protocol information for a non-Windows
    service

type Services struct {
    CreatedAt        string              `json:"created_at,omitempty"`
    OpenServicePorts []*OpenServicePorts `json:"open_service_ports,omitempty"`
    UptimeSeconds    int                 `json:"uptime_seconds,omitempty"`
}
    Services represent the Services running on a Workload

type Sources struct {
    Include [][]Include `json:"include"`
    Exclude []Exclude   `json:"exclude"`
}
    Sources represents the sources query portion of the explorer API

type Src struct {
    IP       string    `json:"ip"`
    Workload *Workload `json:"workload,omitempty"`
}
    Src is the consumer workload details

type Statements struct {
    ChainName  string `json:"chain_name"`
    Parameters string `json:"parameters"`
    TableName  string `json:"table_name"`
}
    Statements are part of a custom IPTables rule

type Status struct {
    AgentHealth              []*AgentHealth     `json:"agent_health,omitempty"`
    AgentHealthErrors        *AgentHealthErrors `json:"agent_health_errors,omitempty"`
    AgentVersion             string             `json:"agent_version,omitempty"`
    FirewallRuleCount        int                `json:"firewall_rule_count,omitempty"`
    FwConfigCurrent          bool               `json:"fw_config_current,omitempty"`
    InstanceID               string             `json:"instance_id,omitempty"`
    LastHeartbeatOn          string             `json:"last_heartbeat_on,omitempty"`
    ManagedSince             string             `json:"managed_since,omitempty"`
    SecurityPolicyAppliedAt  string             `json:"security_policy_applied_at,omitempty"`
    SecurityPolicyReceivedAt string             `json:"security_policy_received_at,omitempty"`
    SecurityPolicyRefreshAt  string             `json:"security_policy_refresh_at,omitempty"`
    SecurityPolicySyncState  string             `json:"security_policy_sync_state,omitempty"`
    Status                   string             `json:"status,omitempty"`
    UID                      string             `json:"uid,omitempty"`
    UptimeSeconds            int                `json:"uptime_seconds,omitempty"`
}
    Status represents the Status of an Agent on a Workload

type SubGroups struct {
    Href string `json:"href"`
    Name string `json:"name,omitempty"`
}
    SubGroups represent SubGroups for Label Groups

type TimestampRange struct {
    FirstDetected string `json:"first_detected"`
    LastDetected  string `json:"last_detected"`
}
    TimestampRange is used to limit queries ranges for the flow detected

type TrafficAnalysis struct {
    Dst            *Dst            `json:"dst"`
    NumConnections int             `json:"num_connections"`
    PolicyDecision string          `json:"policy_decision"`
    ExpSrv         *ExpSrv         `json:"service"`
    Src            *Src            `json:"src"`
    TimestampRange *TimestampRange `json:"timestamp_range"`
}
    TrafficAnalysis represents the response from the explorer API

type TrafficAnalysisRequest struct {
    Sources          Sources          `json:"sources"`
    Destinations     Destinations     `json:"destinations"`
    ExplorerServices ExplorerServices `json:"services"`
    StartDate        time.Time        `json:"start_date,omitempty"`
    EndDate          time.Time        `json:"end_date,omitempty"`
    PolicyDecisions  []string         `json:"policy_decisions"`
    MaxResults       int              `json:"max_results,omitempty"`
}
    TrafficAnalysisRequest represents the payload object for the traffic
    analysis POST request

type TrafficQuery struct {
    SourcesInclude        []string
    SourcesExclude        []string
    DestinationsInclude   []string
    DestinationsExclude   []string
    PortProtoInclude      [][2]int
    PortProtoExclude      [][2]int
    PortRangeInclude      [][2]int
    PortRangeExclude      [][2]int
    ProcessInclude        []string
    WindowsServiceInclude []string
    ProcessExclude        []string
    WindowsServiceExclude []string
    StartTime             time.Time
    EndTime               time.Time
    PolicyStatuses        []string
    MaxFLows              int
}
    TrafficQuery is the struct to be passed to the GetTrafficAnalysis
    function

type UpdatedBy struct {
    Href string `json:"href"`
}
    UpdatedBy represents the UpdatedBy property of an object

type UploadFlowResults struct {
    FlowResps       []FlowUploadResp
    APIResps        []APIResponse
    TotalFlowsInCSV int
}
    UploadFlowResults is the struct returned to the user when using the
    pce.UploadTraffic() method

type Usage struct {
    LabelGroup         bool `json:"label_group"`
    Rule               bool `json:"rule"`
    Ruleset            bool `json:"ruleset"`
    StaticPolicyScopes bool `json:"static_policy_scopes,omitempty"`
}
    Usage covers how a LabelGroup is used in the PCE

type UserLogin struct {
    AuthUsername                string          `json:"auth_username,omitempty"`
    FullName                    string          `json:"full_name,omitempty"`
    Href                        string          `json:"href,omitempty"`
    InactivityExpirationMinutes int             `json:"inactivity_expiration_minutes,omitempty"`
    LastLoginIPAddress          string          `json:"last_login_ip_address,omitempty"`
    LastLoginOn                 string          `json:"last_login_on,omitempty"`
    ProductVersion              *ProductVersion `json:"product_version,omitempty"`
    SessionToken                string          `json:"session_token,omitempty"`
    TimeZone                    string          `json:"time_zone,omitempty,omitempty"`
    Type                        string          `json:"type,omitempty"`
    Orgs                        []*Org          `json:"orgs,omitempty"`
}
    UserLogin represents a user logging in via password to get a session key

type Version struct {
    Version      string `json:"version"`
    Build        int    `json:"build"`
    LongDisplay  string `json:"long_display"`
    ShortDisplay string `json:"short_display"`
}
    Version represents the version of the PCE

type VirtualServer struct {
    Href string `json:"href"`
}
    VirtualServer represents a Virtual Server in the Illumio PCE

type VirtualServers struct {
    Href string `json:"href"`
}
    VirtualServers

type VirtualService struct {
    ApplyTo               string     `json:"apply_to,omitempty"`
    CreatedAt             string     `json:"created_at,omitempty"`
    CreatedBy             *CreatedBy `json:"created_by,omitempty"`
    Description           string     `json:"description,omitempty"`
    ExternalDataReference string     `json:"external_data_reference,omitempty"`
    ExternalDataSet       string     `json:"external_data_set,omitempty"`
    Href                  string     `json:"href,omitempty"`
    IPOverrides           []string   `json:"ip_overrides,omitempty"`
    Labels                []*Label   `json:"labels,omitempty"`
    Name                  string     `json:"name,omitempty"`
    Service               *Service   `json:"service,omitempty"`
    UpdateType            string     `json:"update_type,omitempty"`
    UpdatedAt             string     `json:"updated_at,omitempty"`
    UpdatedBy             *UpdatedBy `json:"updated_by,omitempty"`
}
    A VirtualService represents a Virtual Service in the Illumio PCE

type VirtualServices struct {
    Href string `json:"href"`
}
    VirtualServices

type Vulnerability struct {
    CreatedAt   string     `json:"created_at,omitempty"`
    CreatedBy   *CreatedBy `json:"created_by,omitempty"`
    CveIds      []string   `json:"cve_ids,omitempty"`
    Description string     `json:"description,omitempty"`
    Href        string     `json:"href,omitempty"`
    Name        string     `json:"name,omitempty"`
    Score       int        `json:"score,omitempty"`
    UpdatedAt   string     `json:"updated_at,omitempty"`
    UpdatedBy   *UpdatedBy `json:"updated_by,omitempty"`
}
    Vulnerability represents a vulnerability in the Illumio PCE

type VulnerabilityReport struct {
    Authoritative      bool       `json:"authoritative,omitempty"`
    CreatedAt          string     `json:"created_at,omitempty"`
    CreatedBy          *CreatedBy `json:"created_by,omitempty"`
    Href               string     `json:"href,omitempty"`
    Name               string     `json:"name,omitempty"`
    NumVulnerabilities int        `json:"num_vulnerabilities,omitempty"`
    ReportType         string     `json:"report_type,omitempty"`
    ScannedIps         []string   `json:"scanned_ips,omitempty,omitempty"`
    UpdatedAt          string     `json:"updated_at,omitempty"`
    UpdatedBy          *UpdatedBy `json:"updated_by,omitempty"`
}
    VulnerabilityReport represents a vulnerability report in the Illumio PCE

type WindowsService struct {
    IcmpCode    int    `json:"icmp_code,omitempty"`
    IcmpType    int    `json:"icmp_type,omitempty"`
    Port        int    `json:"port,omitempty"`
    ProcessName string `json:"process_name,omitempty"`
    Protocol    int    `json:"protocol,omitempty"`
    ServiceName string `json:"service_name,omitempty"`
    ToPort      int    `json:"to_port,omitempty"`
}
    WindowsService represents port and protocol information for a Windows
    service

type Workload struct {
    Agent                 *Agent       `json:"agent,omitempty"`
    CreatedAt             string       `json:"created_at,omitempty"`
    CreatedBy             *CreatedBy   `json:"created_by,omitempty"`
    DataCenter            string       `json:"data_center,omitempty"`
    DataCenterZone        string       `json:"data_center_zone,omitempty"`
    DeleteType            string       `json:"delete_type,omitempty"`
    Deleted               *bool        `json:"deleted,omitempty"`
    DeletedAt             string       `json:"deleted_at,omitempty"`
    DeletedBy             *DeletedBy   `json:"deleted_by,omitempty"`
    Description           string       `json:"description,omitempty"`
    ExternalDataReference string       `json:"external_data_reference,omitempty"`
    ExternalDataSet       string       `json:"external_data_set,omitempty"`
    Hostname              string       `json:"hostname,omitempty"`
    Href                  string       `json:"href,omitempty"`
    Interfaces            []*Interface `json:"interfaces,omitempty"`
    Labels                []*Label     `json:"labels,omitempty"`
    Name                  string       `json:"name,omitempty"`
    Online                bool         `json:"online,omitempty"`
    OsDetail              string       `json:"os_detail,omitempty"`
    OsID                  string       `json:"os_id,omitempty"`
    PublicIP              string       `json:"public_ip,omitempty"`
    ServicePrincipalName  string       `json:"service_principal_name,omitempty"`
    ServiceProvider       string       `json:"service_provider,omitempty"`
    Services              []*Services  `json:"services,omitempty"`
    UpdatedAt             string       `json:"updated_at,omitempty"`
    UpdatedBy             *UpdatedBy   `json:"updated_by,omitempty"`
}
    A Workload represents a workload in the PCE

func (w *Workload) ChangeLabel(pce PCE, targetKey, newValue string) (PCE, error)
    ChangeLabel updates a workload struct with new label href. It does not
    call the Illumio API to update the workload in the PCE. Use
    pce.UpdateWorkload() or bulk update for that. The method returns the
    labelMapH in case it needs to create a new label.

func (w *Workload) GetApp(labelMap map[string]Label) Label
    GetApp takes a map of labels with the href string as the key and returns
    the app label for a workload. To get the LabelMap call GetLabelMapH.

func (w *Workload) GetAppGroup(labelMap map[string]Label) string
    GetAppGroup returns the app group string of a workload in the format of
    App | Env. If the workload does not have an app or env label, "NO APP
    GROUP" is returned. Use GetAppGroupL to include the loc label in the app
    group.

func (w *Workload) GetAppGroupL(labelMap map[string]Label) string
    GetAppGroupL returns the app group string of a workload in the format of
    App | Env | Loc. If the workload does not have an app, env, or loc
    label, "NO APP GROUP" is returned. Use GetAppGroup to only use app and
    env in App Group.

func (w *Workload) GetEnv(labelMap map[string]Label) Label
    GetEnv takes a map of labels with the href string as the key and returns
    the env label for a workload. To get the LabelMap call GetLabelMapH.

func (w *Workload) GetLoc(labelMap map[string]Label) Label
    GetLoc takes a map of labels with the href string as the key and returns
    the loc label for a workload. To get the LabelMap call GetLabelMapH.

func (w *Workload) GetMode() string
    GetMode returns the mode of the workloads. Modes are unmanaged, idle,
    build, test, enforced-no, enforced-low, enforced-high.

func (w *Workload) GetRole(labelMap map[string]Label) Label
    GetRole takes a map of labels with the href string as the key and
    returns the role label for a workload. To get the LabelMap call
    GetLabelMapH.

func (w *Workload) LabelsMatch(role, app, env, loc string, labelMap map[string]Label) bool
    LabelsMatch checks if the workload matches the provided labels. Blank
    values ("") for role, app, env, or loc mean no label assigned for that
    key. A single asterisk (*) can be used to represent any in a particular
    key. For example, using "*" for role will return true as long as the
    app, env, and loc match.

func (w *Workload) SanitizeBulkUpdate()
    SanitizeBulkUpdate removes the properites necessary for a bulk update

func (w *Workload) SanitizePut()
    SanitizePut removes the necessary properties to update an unmanaged and
    managed workload

func (w *Workload) SetMode(m string) error
    SetMode adjusts the workload struct to reflect the assigned mode.
    Nothing is changed in the PCE. To reflect the change in the PCE uset
    SetMode method followed by PCE.UpdateWorkload() method

    Valid options: idle, build, test, enforced-no, enforced-low, and
    enforced-high. The enforced options represent no logging, low details,
    and high detail.

SUBDIRECTORIES

        illumioapi_test

```
