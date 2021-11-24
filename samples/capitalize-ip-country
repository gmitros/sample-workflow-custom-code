/**
 * Capitalizes the first letter of every part of a contact's ip country.
 * Before adding this custom code, copy the value of "ip_country" to an intermediate property "ip_country_text_transform".

const IP_COUNTRY_TEXT_TRANSFORM_PROP = "ip_country_text_transform";

const hubspot = require('@hubspot/api-client');

exports.main = (event, callback) => {
  callback(processEvent(event));
};

function processEvent(event) {
  const hubspotClient = new hubspot.Client({ apiKey: process.env.HAPIKEY });
  
  let contactId = event.object.objectId;
  
  hubspotClient.crm.contacts.basicApi
    .getById(contactId, [IP_COUNTRY_TEXT_TRANSFORM_PROP])
    .then(results => {
      let ip_country_text_transform = results.body.properties[IP_COUNTRY_TEXT_TRANSFORM_PROP];

      hubspotClient.crm.contacts.basicApi
        .update(
          contactId,
          {
            properties: {
              [IP_COUNTRY_TEXT_TRANSFORM_PROP]: capitalizeName(ip_country_text_transform)
            }
          }
        )
        .then(updateResults => null);
    });
}

function capitalizeName(name) {
  return name
    .toLowerCase()
    .trim()
    .replace(/\b(\w)/g, s => s.toUpperCase());
}
