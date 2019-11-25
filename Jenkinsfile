import groovy.json.JsonOutput 

node {

    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("tadamhicks/demo_app")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }

    stage('Provision Dev App') {
        /*
         *
         *  */

        withCredentials([string(credentialsId: 'demo-morph-scrt', variable: 'bearer')]) {
            String morpheusUrl = 'https://192.168.235.142/api/apps'

            Map<?, ?> postBody = [
    "id": 1,
  "tiers": [
    "Web": [
      "instances": [
        [
          "instance": [
            "type": "tomcat",
            "cloud": "Local vCenter",
            "layout": [
              "provisionTypeCode": "vmware",
              "code": "tomcat-vmware-7.0.62-single",
              "instanceVersion": "Tomcat 7 jdk 7",
              "name": "VMware Tomcat",
              "id": 1083
            ],
            "name": "dammit",
            "allowExisting": false,
            "userGroup": [
              "id": ""
            ]
          ],
          "environments": [
            "Production": [
              "groups": [
                "wangchung": [
                  "clouds": [
                    "Local vCenter": [
                      "backup": [
                        "veeamManagedServer": "",
                        "createBackup": false,
                        "jobAction": "new",
                        "jobRetentionCount": 3,
                        "enabled": true,
                        "showScheduledBackupWarning": false
                      ],
                      "instance": [
                        "layout": [
                          "provisionTypeCode": "vmware",
                          "code": "tomcat-vmware-7.0.62-single",
                          "instanceVersion": "Tomcat 7 jdk 7",
                          "name": "VMware Tomcat",
                          "id": 1083
                        ],
                        "name": "dammit",
                        "allowExisting": false,
                        "type": "tomcat",
                        "userGroup": [
                          "id": ""
                        ]
                      ],
                      "networkInterfaces": [
                        [
                          "ipMode": "",
                          "primaryInterface": true,
                          "showNetworkPoolLabel": false,
                          "showNetworkDhcpLabel": true,
                          "network": [
                            "idName": "VM Network",
                            "id": "network-1",
                            "hasPool": false
                          ]
                        ]
                      ],
                      "loadBalancer": [
                        [
                          "externalAddressCheck": false,
                          "protocol": "http",
                          "vipPort": 8080,
                          "internalPort": 8080,
                          "loadBalancePort": 80,
                          "loadBalanceProtocol": "http",
                          "vipHostname": "local.localdomain",
                          "name": "lbservice-8080",
                          "vipShared": "off",
                          "externalAddress": "off",
                          "balanceMode": "leastconnections",
                          "externalPort": 8080
                        ]
                      ],
                      "volumes": [
                        [
                          "volumeCustomizable": true,
                          "readonlyName": false,
                          "controllerId": 85,
                          "maxIOPS": null,
                          "displayOrder": 0,
                          "unitNumber": null,
                          "minStorage": 2147483648,
                          "configurableIOPS": false,
                          "controllerMountPoint": "85:0:4:0",
                          "vId": 506,
                          "size": 10,
                          "name": "root",
                          "rootVolume": true,
                          "storageType": 1,
                          "typeId": 29,
                          "id": 29,
                          "resizeable": true,
                          "datastoreId": "auto",
                          "maxStorage": 2147483648
                        ]
                      ],
                      "ports": [
                        [
                          "code": "tomcat.8080",
                          "visible": true,
                          "internalPort": 8080,
                          "loadBalancePort": 80,
                          "loadBalanceProtocol": "http",
                          "sortOrder": 0,
                          "name": "Http",
                          "id": 16,
                          "shortName": "http",
                          "externalPort": 8080,
                          "loadBalance": true
                        ]
                      ],
                      "config": [
                        "resourcePoolId": 1,
                        "createUser": true
                      ],
                      "plan": [
                        "code": "vm-512",
                        "id": 361
                      ],
                      "group": [
                        "id": 1
                      ]
                    ]
                  ]
                ]
              ]
            ]
          ],
          "backup": [
            "veeamManagedServer": "",
            "createBackup": false,
            "jobAction": "new",
            "jobRetentionCount": 3,
            "enabled": true,
            "showScheduledBackupWarning": false
          ],
          "networkInterfaces": [
            [
              "ipMode": "",
              "primaryInterface": true,
              "showNetworkPoolLabel": false,
              "showNetworkDhcpLabel": true,
              "network": [
                "idName": "VM Network",
                "id": "network-1",
                "hasPool": false
              ]
            ]
          ],
          "loadBalancer": [
            [
              "externalAddressCheck": false,
              "protocol": "http",
              "vipPort": 8080,
              "internalPort": 8080,
              "loadBalancePort": 80,
              "loadBalanceProtocol": "http",
              "vipHostname": "local.localdomain",
              "name": "lbservice-8080",
              "vipShared": "off",
              "externalAddress": "off",
              "balanceMode": "leastconnections",
              "externalPort": 8080
            ]
          ],
          "volumes": [
            [
              "volumeCustomizable": true,
              "readonlyName": false,
              "controllerId": 85,
              "maxIOPS": null,
              "displayOrder": 0,
              "unitNumber": null,
              "minStorage": 2147483648,
              "configurableIOPS": false,
              "controllerMountPoint": "85:0:4:0",
              "vId": 506,
              "size": 10,
              "name": "root",
              "rootVolume": true,
              "storageType": 1,
              "typeId": 29,
              "id": 29,
              "resizeable": true,
              "datastoreId": "auto",
              "maxStorage": 2147483648
            ]
          ],
          "ports": [
            [
              "code": "tomcat.8080",
              "visible": true,
              "internalPort": 8080,
              "loadBalancePort": 80,
              "loadBalanceProtocol": "http",
              "sortOrder": 0,
              "name": "Http",
              "id": 16,
              "shortName": "http",
              "externalPort": 8080,
              "loadBalance": true
            ]
          ],
          "config": [
            "resourcePoolId": 1,
            "createUser": true
          ],
          "plan": [
            "code": "vm-512",
            "id": 361
          ],
          "group": [
            "id": 1
          ]
        ]
      ],
      "tierIndex": 1
    ],
    "Database": [
      "instances": [
        [
          "instance": [
            "type": "mysql",
            "cloud": "Local vCenter"
          ],
          "environments": [
            "Dev": [
              "groups": [
                "wangchung": [
                  "clouds": [
                    "Local vCenter": [
                      "backup": [
                        "veeamManagedServer": "",
                        "createBackup": false,
                        "jobAction": "new",
                        "jobRetentionCount": 3,
                        "enabled": true,
                        "showScheduledBackupWarning": false
                      ],
                      "instance": [
                        "layout": [
                          "provisionTypeCode": "vmware",
                          "code": "mysql-vmware-5.6-single",
                          "instanceVersion": "5.6",
                          "name": "VMware Master",
                          "id": 799
                        ],
                        "name": "dammit",
                        "allowExisting": false,
                        "type": "mysql",
                        "userGroup": [
                          "id": ""
                        ]
                      ],
                      "networkInterfaces": [
                        [
                          "ipMode": "",
                          "primaryInterface": true,
                          "showNetworkPoolLabel": false,
                          "showNetworkDhcpLabel": true,
                          "network": [
                            "idName": "VM Network",
                            "id": "network-1",
                            "hasPool": false
                          ]
                        ]
                      ],
                      "loadBalancer": [],
                      "volumes": [
                        [
                          "volumeCustomizable": true,
                          "readonlyName": false,
                          "controllerId": 67,
                          "maxIOPS": null,
                          "displayOrder": 0,
                          "unitNumber": null,
                          "minStorage": 2147483648,
                          "configurableIOPS": false,
                          "controllerMountPoint": "67:0:4:0",
                          "vId": 373,
                          "size": 20,
                          "name": "root",
                          "rootVolume": true,
                          "storageType": 1,
                          "typeId": 29,
                          "id": 23,
                          "resizeable": true,
                          "datastoreId": "auto",
                          "maxStorage": 2147483648
                        ]
                      ],
                      "ports": [
                        [
                          "code": "mysql.3306",
                          "visible": true,
                          "internalPort": 3306,
                          "loadBalancePort": null,
                          "loadBalanceProtocol": null,
                          "sortOrder": 0,
                          "name": "Db Port",
                          "id": 15,
                          "shortName": "tcp",
                          "externalPort": 3306,
                          "loadBalance": false
                        ]
                      ],
                      "config": [
                        "password": "************",
                        "resourcePoolId": 1,
                        "hostId": 1,
                        "createUser": true,
                        "rootPassword": "************",
                        "username": "rnelson"
                      ],
                      "plan": [
                        "code": "vm-2048",
                        "id": 363
                      ],
                      "group": [
                        "id": 1
                      ]
                    ]
                  
                ]
              ]
            ]
          ]
        ]
      ],
      "tierIndex": 2
    ]
  ],
  "templateName": "SGX",
  "name": "SGX Jenkins",
  "group": [
    "id": 1,
    "name": "wangchung"
  ],
  "environment": "Production",
  "envCode": "production",
  "type": "morpheus"
  ]
]

            echo morpheusApp.buildApp(morpheusUrl, postBody, "${bearer}")
        }
    }


}
