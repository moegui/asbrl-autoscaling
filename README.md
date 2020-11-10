ASBRL-AUTOSCALING
=========

Create a CloudFormation Template to Deploy AutoScalingGroup stack.

Requirements
------------

None

Role Variables
--------------

- TEMPLATE_DEST: (String)
- TAGS:
    - RELEASE: (String)
    - ENVIRONMENT_TYPE: (String)
- LAUNCH_TEMPLATES: (List)
  - NAME: (String)
  - OUTPUT: (Boolean)
  - INSTANCE_PROFILE: (String)
  - SECURITY_GROUPS: (List)
    - NAME: (String)
  - EBS:
    - PRIORIZED_DISK:
      - ENABLED: (Boolean)
  - TAGS: (List)
    - Key: (String)
    - Value: (String)
- AUTOSCALING_GROUPS: (List)
  - NAME: (String)
  - LAUNCH_TEMPLATE:
    - NAME: (String)
  - TARGET_GROUPS: (List)
    - NAME: (String)
    - LB_NAME: (String)
  
Dependencies
------------

None

Example Playbook
----------------

        - name: Generate {{EnvironmentType}} cf-autoscalinggroup
          include_role:
            name: asbrl-autoscaling
          vars:
            TEMPLATE_DEST: ./artifacts/{{EnvironmentType}}/cf-rabbitstack-autoscalinggroup.yml
            TAGS:
              RELEASE: "{{Release}}"
              ENVIRONMENT_TYPE: "{{EnvironmentType}}"
            LAUNCH_TEMPLATES:
            - NAME: Rabbit
              OUTPUT: false
              INSTANCE_PROFILE: Node
              SECURITY_GROUPS:
              - NAME: Ec2Internal
              - NAME: Ec2Custom
              TAGS:
              - Key: tag1
                Value: value1
            AUTOSCALING_GROUPS:
            - NAME: Rabbit
              LAUNCH_TEMPLATE:
                NAME: Rabbit
              TARGET_GROUPS:
              - NAME: Client
                LB_NAME: Rabbit
              - NAME: Mng
                LB_NAME: Rabbit

License
-------

BSD

Author Information
------------------

Moegui.com
